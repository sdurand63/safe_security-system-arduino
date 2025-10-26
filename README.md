# safe-security-system
Lien du circuit de la simulation Tinkercad/link of the Tinkercad circuit : [simulation circuit](https://www.tinkercad.com/things/9fMGPyPVTWV-strongbox-3000-circuit)

## French description
Ce projet implémente un système de sécurité à authentification multi-niveaux pour un coffre-fort, développé sur Arduino via Tinkercad. Le système intègre un lecteur de carte basé sur la détection de tension et combine jusqu'à 4 méthodes d'authentification différentes pour créer 4 niveaux de sécurité distincts.

**Fonctionnement du Système** :  
1. Détection de Carte : L'utilisateur passe une carte, le système lit la tension via la broche analogique A0
2. Authentification Séquentielle : L'utilisateur complète les méthodes d'authentification requises dans l'ordre
3. Retour Visuel : Les LEDs indiquent la progression et l'étape d'authentification actuelle
4. Accès au Coffre : En cas de succès, la LED bleue s'allume et le coffre s'ouvre pendant 10 secondes, puis se referme

**Modes d'authentification** :  
**MA1** : Quiz de sécurité 
4 questions personnelles avec choix multiples :
- Prénom du chien
- Année de découverte de l'Amérique
- Prénom de la belle-mère
- Note au bac de philosophie  

**MA2** : Code PIN
Saisie d'un code à 4 chiffres (par défaut : 2294)
Sécurité : 4 tentatives erronées déclenchent un blocage de 30 secondes avec clignotement des LEDs  
**MA3** : Scan Rétinien
Authentification biométrique simulée par scan rétinien  
**MA4** : Scan Digital
Authentification biométrique simulée par empreinte digitale  

## English description
This project implements a multi-level authentication security system for a safe, developed on Arduino using Tinkercad. The system features a card reader based on voltage detection and combines up to 4 different authentication methods to create 4 distinct security levels.

**System Operation** : 
1. Card Detection: User swipes a card, system reads the voltage via analog pin A0
2. Sequential Authentication: User completes required authentication methods in order
3. Visual Feedback: LEDs indicate progress and current authentication step
4. Safe Access: Upon successful completion, blue LED lights up and safe opens for 10 seconds

**Authentification methods (MA)** :  
**MA1** : Security Quiz
4 personal questions with multiple-choice answers:
- Dog's name
- Discovery of America date
- Mother-in-law's first name
- Philosophy exam grade
Security: 4 wrong answers trigger a 30-second lockout

**MA2** : PIN Code
4-digit code entry (default: 2294)
Security: 4 wrong attempts trigger a 30-second lockout with LED blinking  
**MA3** : Retinal Scan
Simulated biometric authentication via retinal scan  
**MA4** : Fingerprint Scan
Simulated biometric authentication via fingerprint scan  

