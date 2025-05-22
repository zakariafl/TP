# Rapport de TP : Injection de Dépendances et Inversion de Contrôle (IoC)

##  Objectif

Mettre en œuvre l’injection de dépendances en Java à travers plusieurs approches :  
- Instanciation **statique**
- Instanciation **dynamique** (réflexion)
- Utilisation du framework **Spring** (version XML et annotations)

Ces techniques illustrent les principes d’**Inversion de Contrôle (IoC)** et permettent de construire des architectures modulaires, testables et évolutives.

---

##  Structure du Projet

```
src/
├── net.falkou.dao
│   ├── Idao.java
│   ├── DaoImpl.java
├── net.falkou.ext
│   └── DaoImplV2.java
├── net.falkou.metier
│   ├── IMetier.java
│   └── MetierImpl.java
├── net.falkou.pres
│   ├── Pres1.java
│   ├── Pres2.java
│   ├── PresSpringXML.java
│   ├── PresSpringAnnotation.java
│   └── config.xml
```

---

##  Détails des Composants

### 📁 `dao`

- **IDao.java** : Interface pour accéder aux données via `getData()`
- **DaoImpl.java** : Accès aux données (version base de données)
- **DaoImplV2.java** : Version alternative (capteur)

### 📁 `metier`

- **IMetier.java** : Interface métier avec `calcul()`
- **MetierImpl.java** : Implémentation qui dépend d’un `IDao`

### 📁 `presentation`

- **Pres1.java** : Injection **statique**
- **Pres2.java** : Injection **dynamique** via réflexion
- **PresSpringXML.java** : Injection via **Spring XML**
- **PresSpringAnnotation.java** : Injection via **Spring avec annotations**

---

##  Exécution

### ▶️ 1. Instanciation Statique

```bash
java net.falkou.pres.Pres1
```

### ▶️ 2. Instanciation Dynamique (avec `config.txt`)

**Exemple de contenu de `config.txt` :**
```
net.falkou.dao.DaoImpl
net.falkou.metier.MetierImpl
```


```bash
java net.falkou.pres.Pres2
```

### ▶️ 3. Spring (XML)

```bash
java net.falkou.presentation.PresSpringXML
```

Assurez-vous que `config.xml` est bien placé dans le classpath.

### ▶️ 4. Spring (Annotations)

```bash
java net.falkou.presentation.PresSpringAnnotation
```

---

##  Fichier de Configuration Spring (XML)

```xml
<!-- config.xml -->
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
                           https://www.springframework.org/schema/beans/spring-beans.xsd">

    <bean id="d" class="net.falkou.dao.DaoImpl"/>
    <bean id="metier" class="net.falkou.metier.MetierImpl">
        <property name="dao" ref="d"/>
        <constructor-arg ref="d"/>
    </bean>
</beans>
```

---

##  Comparaison des Méthodes d’Injection

| Méthode                  | Couplage      | Avantages                        | Inconvénients                  |
|--------------------------|---------------|----------------------------------|--------------------------------|
| **Instanciation statique**    | Fort          | Simple et directe                | Peu flexible, difficile à maintenir |
| **Instanciation dynamique**   | Moyen-faible  | Flexible (configurable)          | Plus complexe à mettre en œuvre |
| **Spring XML**                | Faible        | Configuration claire et externe  | Dépendance au fichier XML       |
| **Spring Annotations**        | Très faible   | Moderne, léger, automatique      | Nécessite Spring et annotations |

---

## ✅ Conclusion

Ce TP met en évidence l'intérêt des concepts **IoC** et **DI** pour une architecture souple et maintenable.  
L'utilisation de **Spring** (XML ou annotations) est recommandée dans les projets réels pour une gestion optimale des dépendances.

---

## Auteur


**Zakaria Falkou**  
M1 SDIA – 2025  
