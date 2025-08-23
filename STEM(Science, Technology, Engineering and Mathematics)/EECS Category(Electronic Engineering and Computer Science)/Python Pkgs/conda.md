# conda's logic

- [‎Gemini - Python Qt VISA + MSO and conda's logic](https://g.co/gemini/share/2e61710af469) 
- [‎Gemini - Conda 链接与空间占用解释](https://g.co/gemini/share/9231802250f0)  

在`conda install`的过程中, `conda`先将各个`pkg`放进其软件目录`cache to dir: pkgs`中, 而后链接到环境中`link to env: my_env`. 

# conda cmd

### 📁 Step 2: Create & Manage Environments

#### 🔹 Create a new environment

`conda create --name myenv python=3.10`

This creates a new environment named `myenv` with Python 3.10.

#### 🔹 Activate environment

`conda activate myenv`

#### 🔹 Deactivate environment

`conda deactivate`

#### 🔹 Remove environment

`conda remove --name myenv --all`

---

### 📦 Step 3: Install Packages

#### 🔹 Install a package (e.g., numpy)

`conda install numpy`

#### 🔹 Install multiple packages

`conda install pandas matplotlib scikit-learn`

#### 🔹 Search for a package

`conda search package-name`

#### 🔹 Update a package

`conda update numpy`

---

### 📄 Step 4: List Things

#### 🔹 List all environments

`conda env list`

#### 🔹 List all installed packages in the environment

`conda list`

---

### 🌐 Step 5: Using Channels

Channels are sources for packages. The default is `defaults`, but `conda-forge` is popular and often has newer packages.

`conda install -c conda-forge opencv`

---

### 📦 Export/Import Environments

#### 🔹 Export current environment to a `.yml` file

`conda env export > environment.yml`

#### 🔹 Create an environment from a `.yml` file

`conda env create -f environment.yml`

---

# conda pythonpath

- [zhihu - python，自己做的.py文件想做成本地库，在本机任何一个文件中直接import，怎么实现？放哪？](https://www.zhihu.com/question/661124529) 

````powershell
conda env config vars set PYTHONPATH=/a/b
````
