
# Comment installer mfa pour ssh

## Étape 1 : Installer `google-authenticator`

### Sur Debian/Ubuntu :

```bash
sudo apt install libpam-google-authenticator
```

## Étape 2 : Configurer Google Authenticator pour chaque utilisateur

### 1. Connecte-toi en SSH avec l’utilisateur concerné :

```bash
ssh user@your-server
```

### 2. Lance la configuration :

```bash
google-authenticator
```

| Do you want authentication tokens to be time-based?  →| yes
| --------------------------------------------------- |------- |              
La question qui permet de générer :

* Un **QR code** à scanner avec ton app Google Authenticator
* Ou un **code secret** que tu peux entrer manuellement dans ton appli si besoin
* Puis tu rentre le code de l'app qui après de donne → 5 **codes de secours** (à sauvegarder !)


Puis les questions suivantes
| Question                                                        | Réponse recommandée |
| --------------------------------------------------------------- | ------------------- |
| Do you want me to update your "\~/.google\_authenticator" file? | **yes**             |
| Do you want to disallow multiple uses of the same token?        | **yes**             |
| Do you want to increase the default window?                     | **no**              |
| Do you want to enable rate-limiting?                            | **yes**             |

>  Le fichier `~/.google_authenticator` est alors créé et contient tes infos MFA.

---

##  Étape 3 : Configurer PAM (Pluggable Authentication Module)

Ouvre le fichier :

```bash
sudo nano /etc/pam.d/sshd
```

Ajoute cette ligne **au début du fichier** (ou après les `@include common-auth` sur Ubuntu) :

```bash
auth required pam_google_authenticator.so
```

et à la fin du fichier en dessous de ```@include common-password```

```bash
auth required pam_google_authenticator.so nullok

authc required pam_permit.so

```

>  Attention : Ne supprime pas les lignes existantes, sinon tu risques de casser l’authentification SSH.

---

##  Étape 4 : Configurer le service SSH pour activer MFA

Ouvre la configuration du serveur SSH :

```bash
sudo nano /etc/ssh/sshd_config
```

Vérifie ou modifie les lignes suivantes :

```bash
PermitRootLogin yes ## Si besoin de se co au root directement , genre ssh root@192.168....  

...
KbdIntercativeAuthentication yes ## vérifier bien le yes  
...
UsePAM yes ## de même


```
##  Étape 5 : Redémarrer SSH

```bash
sudo systemctl restart sshd
```

---

## Étape 5 : Tester la connexion SSH

Dans un **autre terminal** ou sur une autre machine :

```bash
ssh user@your-server
```

Tu devrais :

1. T'authentifier avec ton **mot de passe**
2. Voir un prompt comme :

```bash
Verification code:

## j'ai du le rentré 2fois pour ma part jsp pk , mais ça a marché
```

 3. Entre le code généré par ton app Google Authenticator.


---

##  Sécurité supplémentaire

* **Sauvegarde les codes de secours !**
* Tu peux activer `Fail2Ban` pour bloquer les IP après plusieurs échecs
* Crée un second utilisateur sans MFA (admin temporaire) au cas où tu perds l’accès

---

##  Désactivation (si besoin)

Pour désactiver MFA :

1. Supprime/modifie la ligne dans `/etc/pam.d/sshd`
2. Ajuste `UsePAM no` à `UsePAM yes` dans `/etc/ssh/sshd_config`
3. Redémarre `sshd`

---

## Source pour ce doc  
 • [une vidéo youtube](https://youtu.be/ikXRu-9cDn4?si=N5Bzw9UJyw-FCeMv "Enable MFA on SSH")

