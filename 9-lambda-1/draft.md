---

## <a href="#introduction">**1. Introduction**</a>
   - <a href="#services-que-nous-allons-utiliser">Services que nous allons utiliser</a>
   - <a href="#de-quoi-avons-nous-besoin">De quoi avons-nous besoin ?</a>
   - <a href="#plus-de-details">Plus de détails : De quoi avons-nous besoin pour créer une application web simple ?</a>

## <a href="#architecture">**2. Architecture**</a>

## <a href="#etape-1-aws-amplify">**3. Étape 1 : AWS Amplify**</a>
   - <a href="#creer-un-fichier-html">3.1. Créer un fichier HTML</a>
     - <a href="#creer-un-fichier-texte-simple">3.1.1. Créer un fichier texte simple</a>
     - <a href="#renommer-le-fichier">3.1.2. Renommer le fichier texte en fichier HTML (index.html)</a>
     - <a href="#ouvrir-le-fichier">3.1.3. Ouvrir le fichier avec Notepad++</a>
     - <a href="#ajouter-le-code-html">3.1.4. Ajouter le code de la page HTML</a>
     - <a href="#compresser-le-fichier">3.1.5. Compresser le fichier en ZIP</a>
   - <a href="#deployer-le-site">3.2. Déployer le site dans AWS Amplify</a>
     - <a href="#chercher-le-service-amplify">3.2.1. Chercher le service AWS Amplify</a>
     - <a href="#demarrer-le-service">3.2.2. Démarrer le service AWS Amplify</a>
     - <a href="#deployer-sans-git">3.2.3. Déployer sans Git provider ou référentiel Git</a>
     - <a href="#drag-and-drop">3.2.4. Effectuer un Drag and Drop</a>
     - <a href="#sauvegarder-et-deployer">3.2.5. Sauvegarder et déployer</a>
     - <a href="#ouvrir-le-lien-du-domaine">3.2.6. Ouvrir le lien du Domaine sur votre navigateur</a>
     - <a href="#observer-la-page-html">3.2.7. Observer votre page HTML</a>

## <a href="#etape-2-aws-lambda">**4. Étape 2 : AWS Lambda**</a>
   - <a href="#ouvrir-le-service-lambda">4.1. Ouvrir le service AWS Lambda</a>
   - <a href="#creer-une-fonction-lambda">4.2. Créer une fonction Lambda "PowerOfMathFunction"</a>
   - <a href="#copier-et-coller-le-code">4.3. Copier et coller le code Python</a>
   - <a href="#sauvegarder-la-fonction">4.4. Sauvegarder</a>
   - <a href="#deployer-la-fonction">4.5. Déployer</a>
   - <a href="#configurer-un-evenement-test">4.6. Configurer un événement de test</a>
   - <a href="#finaliser-et-coller-le-code">4.7. Finaliser l'événement de test et copier/coller le code</a>
   - <a href="#tester-la-fonction">4.8. Tester</a>

## <a href="#etape-3-amazon-api-gateway">**5. Étape 3 : Amazon API Gateway**</a>

## <a href="#etape-4-amazon-dynamodb">**6. Étape 4 : Amazon DynamoDB**</a>

## <a href="#etape-5-aws-iam">**7. Étape 5 : AWS Gestion des identités et des accès (IAM)**</a>

## <a href="#etape-6-retour-amplify">**8. Étape 6 : AWS Amplify**</a>



# **Projet AWS - Concevoir et construire une application Web AWS de bout en bout à partir de zéro, étape par étape**

---

## [**1. Introduction**](#introduction)
   - [Services que nous allons utiliser](#services)
   - [De quoi avons-nous besoin ?](#besoin)
   - [Plus de détails : De quoi avons-nous besoin pour créer une application web simple ?](#details)

## [**2. Architecture**](#architecture)

## [**3. Étape 1 : AWS Amplify**](#etape1)
   - [3.1. Créer un fichier HTML](#fichier-html)
     - [3.1.1. Créer un fichier texte simple](#fichier-texte-simple)
     - [3.1.2. Renommer le fichier texte en fichier HTML (index.html)](#renommer-fichier)
     - [3.1.3. Ouvrir le fichier avec Notepad++](#ouvrir-notepad)
     - [3.1.4. Ajouter le code de la page HTML](#ajouter-code-html)
     - [3.1.5. Compresser le fichier en ZIP](#compresser-fichier)
   - [3.2. Déployer le site dans AWS Amplify](#deployer-site-amplify)
     - [3.2.1. Chercher le service AWS Amplify](#chercher-service)
     - [3.2.2. Démarrer le service AWS Amplify](#demarrer-service)
     - [3.2.3. Déployer sans Git provider ou référentiel Git](#deployer-sans-git)
     - [3.2.4. Effectuer un Drag and Drop](#drag-and-drop)
     - [3.2.5. Sauvegarder et déployer](#sauvegarder-deployer)
     - [3.2.6. Ouvrir le lien du Domaine sur votre navigateur](#ouvrir-lien)
     - [3.2.7. Observer votre page HTML](#observer-page-html)

## [**4. Étape 2 : AWS Lambda**](#etape2)
   - [4.1. Ouvrir le service AWS Lambda](#ouvrir-lambda)
   - [4.2. Créer une fonction Lambda "PowerOfMathFunction"](#creer-fonction-lambda)
   - [4.3. Copier et coller le code Python](#copier-code-python)
   - [4.4. Sauvegarder](#sauvegarder)
   - [4.5. Déployer](#deployer)
   - [4.6. Configurer un événement de test](#configurer-test)
   - [4.7. Finaliser l'événement de test et copier/coller le code](#finaliser-coller-code)
   - [4.8. Tester](#tester)

## [**5. Étape 3 : Amazon API Gateway**](#etape3)

## [**6. Étape 4 : Amazon DynamoDB**](#etape4)

## [**7. Étape 5 : AWS Gestion des identités et des accès (IAM)**](#etape5)

## [**8. Étape 6 : AWS Amplify**](#etape6)

---




