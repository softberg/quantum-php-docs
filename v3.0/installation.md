# Installation

This guide walks you through installing and running a new Quantum PHP project.

### 🔧 Requirements

Make sure your environment includes:

* **PHP 7.4+**&#x20;
* **PHP extensions**:
  * PDO
  * JSON
  * OpenSSL
  * bcmath, curl, fileinfo, simplexml (as required by framework)&#x20;
* **Composer** installed and accessible globally

### 🚀 Installation Steps

1.  **Create a new project**

    ```bash
    composer create-project quantum/project my-project
    ```


2.  **Navigate into the project directory**\


    ```
    cd my-project
    ```


3.  **Start the development server**

    ```bash
    php qt serve
    ```

    \
    A built-in server will launch (typically at `http://localhost:8000/`)

### ✅ Verification

You should now see the Quantum default welcome page. That confirms your installation was successful!
