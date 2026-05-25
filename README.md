# ⭐ LAB-23 | JNI App — Développement Android avec JNI

Une application Android démontrant l'utilisation de **JNI (Java Native Interface)** pour appeler du code natif **C++** depuis Java via le **NDK Android**, avec configuration CMake et affichage des résultats en temps réel.

---

## ✨ Fonctionnalités

- 🔗 **Appels JNI Java → C++** — invocation de méthodes natives depuis Java
- 🧮 **Opérations natives** — calculs effectués côté C++ et retournés à Java
- 🛠️ **Configuration CMake** — build du code natif via `CMakeLists.txt`
- 📦 **Chargement dynamique** — chargement de la bibliothèque native via `System.loadLibrary()`
- 📋 **Déclaration native** — méthodes Java déclarées `native` et implémentées en C++
- 🪵 **Logs natifs** — vérification des appels natifs via `__android_log_print` dans Logcat
- 📱 **Interface XML** — affichage des résultats natifs dans l'UI Android

---

## 🛠️ Stack technique

| Composant | Technologie |
|---|---|
| Langage Java | Java |
| Langage natif | C++ |
| Build natif | CMake |
| Interface native | JNI (Java Native Interface) |
| NDK | Android NDK |
| UI | XML Layouts |
| Architecture | Single Activity |
| Build system | Gradle (Kotlin DSL) |

---

## 📁 Architecture du projet

```bash
ensa.ma.jni
├── MainActivity.java                        # Activité principale + appels JNI
├── res/
│   └── layout/
│       └── activity_main.xml               # Interface utilisateur XML
└── cpp/
    ├── CMakeLists.txt                       # Configuration de la bibliothèque native
    └── native-lib.cpp                       # Implémentation des méthodes C++ exposées via JNI
```

---

## 📦 Dépendances & Configuration

```kotlin
// build.gradle.kts
android {
    defaultConfig {
        externalNativeBuild {
            cmake {
                cppFlags("-std=c++17")
            }
        }
    }
    externalNativeBuild {
        cmake {
            path("src/main/cpp/CMakeLists.txt")
            version("3.22.1")
        }
    }
}
```

```cmake
# CMakeLists.txt
cmake_minimum_required(VERSION 3.22.1)
project("jni")

add_library(
    native-lib
    SHARED
    native-lib.cpp
)

find_library(log-lib log)

target_link_libraries(
    native-lib
    ${log-lib}
)
```

---

## 🧠 Concepts Android abordés

- 📌 **JNI (Java Native Interface)** — pont entre Java et C++
- 📌 **NDK (Native Development Kit)** — compilation du code C/C++ pour Android
- 📌 **CMake** — outil de build pour les bibliothèques natives
- 📌 Déclaration `native` en Java et convention de nommage `Java_packageName_ClassName_methodName`
- 📌 Types JNI : `jstring`, `jint`, `jdouble`, `jboolean`, `jobject`, etc.
- 📌 `System.loadLibrary()` — chargement de la bibliothèque `.so` au runtime
- 📌 `__android_log_print` — journalisation native dans Logcat
- 📌 `JNIEnv*` et `jobject` — paramètres obligatoires de toute méthode JNI
- 📌 `extern "C"` — désactivation du name-mangling C++ pour compatibilité JNI
- 📌 `JNIEXPORT` / `JNICALL` — macros de déclaration des fonctions exportées

---

## 🔄 Fonctionnement

1. L'application charge la bibliothèque native au démarrage via `System.loadLibrary("native-lib")`
2. `MainActivity` déclare les méthodes `native` en Java
3. Ces méthodes sont implémentées en C++ dans `native-lib.cpp`
4. CMake compile le code C++ en une bibliothèque partagée `.so`
5. L'appel JNI traverse la couche JVM → NDK → C++
6. Le résultat est renvoyé en Java et affiché dans l'interface
7. Les logs natifs sont visibles dans Logcat via `adb logcat`

---

## 📱 Interface

- **Activité principale** affichant :
  - Résultats des appels natifs C++ en temps réel
  - Valeurs retournées par les fonctions JNI
  - Boutons déclenchant les appels vers le code natif

---

## Logs de JNI:

<img width="1280" height="93" alt="LAB23-1" src="https://github.com/user-attachments/assets/c8f44da8-445b-4f86-9f1c-9f8448c88937" />

## Demo:

https://github.com/user-attachments/assets/4c467557-6028-492c-b4db-76cd84947703

---

## 🎯 Objectif pédagogique

Ce laboratoire montre comment :

- Intégrer du code natif **C++** dans une application Android via **JNI**
- Configurer le **NDK** et **CMake** dans un projet Android Studio
- Respecter la **convention de nommage JNI** pour la résolution automatique des méthodes
- Gérer les **types JNI** et la conversion entre types Java et C++
- Utiliser **Logcat** pour déboguer le code natif
- Comprendre le pipeline de compilation : Java → `.class` → JNI bridge → C++ → `.so`

---

## 👨‍💻 Auteur

**Mourad EL OUATIK** | Réalisé dans le cadre du **Lab 23 Android** | Programmation & Sécurité des Applications Mobile
