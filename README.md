---
description: This guide walks you through installing and running a new Quantum PHP project.
icon: hand-wave
---

# Installation

### Requirmens

Make sure your environment includes:

* **PHP 7.4+**
* **PHP extensions**:
  * PDO
  * JSON
  * OpenSSL
  * bcmath, curl, fileinfo, simplexml
* **Composer** installed and accessible global

### 🚀 Installation Steps

**1. Create project**

```bash
composer create-project quantum/project my-project
```

**2. Navigate into the project directory**

```bash
$ cd my-project
```

**3. Start the development server**

```bash
$ php qt serve
```

A built-in server will launch (typically at `http://localhost:8000/`)

###
