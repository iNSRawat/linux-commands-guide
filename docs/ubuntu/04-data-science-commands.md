# Data Science Commands for Ubuntu

Essential commands for data science workflows on Ubuntu.

## Python & Package Management

### Python Version Management
```bash
python3 --version
python3 -V
which python3

# Install specific Python version
sudo apt install python3.10
sudo update-alternatives --install /usr/bin/python3 python3 /usr/bin/python3.10 1
```

### pip - Python Package Manager
```bash
pip3 --version
pip3 install package-name
pip3 install pandas numpy scipy
pip3 install -r requirements.txt
pip3 install --upgrade package-name
pip3 uninstall package-name
pip3 list
pip3 freeze > requirements.txt
pip3 show package-name
```

## Virtual Environments

### venv - Built-in Virtual Environment
```bash
# Create virtual environment
python3 -m venv myenv
python3 -m venv venv

# Activate
source myenv/bin/activate

# Deactivate
deactivate

# Delete
rm -rf myenv
```

### Conda - Anaconda Environment Manager
```bash
# Install Miniconda
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
bash Miniconda3-latest-Linux-x86_64.sh

# Create environment
conda create -n myenv python=3.10
conda create -n ds-env pandas numpy scikit-learn

# Activate/Deactivate
conda activate myenv
conda deactivate

# List environments
conda env list

# Install packages
conda install pandas
conda install -c conda-forge package-name

# Export/Import environment
conda env export > environment.yml
conda env create -f environment.yml

# Remove environment
conda env remove -n myenv
```

## Jupyter Notebook

### Installation & Usage
```bash
# Install
pip3 install jupyter
pip3 install jupyterlab

# Start Jupyter Notebook
jupyter notebook
jupyter notebook --port=8888
jupyter notebook --no-browser

# Start JupyterLab
jupyter lab

# List running servers
jupyter notebook list

# Convert notebooks
jupyter nbconvert --to html notebook.ipynb
jupyter nbconvert --to python notebook.ipynb
jupyter nbconvert --to pdf notebook.ipynb
```

## Essential Data Science Libraries

### Installation Commands
```bash
# Core data science stack
pip3 install numpy pandas scipy matplotlib seaborn

# Machine learning
pip3 install scikit-learn
pip3 install tensorflow
pip3 install torch torchvision

# Deep learning
pip3 install keras

# Data visualization
pip3 install plotly
pip3 install bokeh

# Jupyter extensions
pip3 install jupyter_contrib_nbextensions
jupyter contrib nbextension install --user

# Streamlit for dashboards
pip3 install streamlit

# Complete data science bundle
pip3 install numpy pandas scipy matplotlib seaborn scikit-learn jupyter
```

## Working with Data Files

### CSV Operations
```bash
# View CSV
head data.csv
tail data.csv
less data.csv

# Count rows
wc -l data.csv

# View specific columns
cut -d',' -f1,3 data.csv

# Sort CSV
sort -t',' -k2 data.csv

# Remove duplicates
sort -u data.csv

# Search in CSV
grep "pattern" data.csv
```

### Using Python for Quick Data Tasks
```bash
# Quick Python one-liners
python3 -c "import pandas as pd; print(pd.read_csv('data.csv').head())"
python3 -c "import pandas as pd; df=pd.read_csv('data.csv'); print(df.shape)"
python3 -c "import pandas as pd; print(pd.read_csv('data.csv').describe())"
```

## GPU & CUDA (for Deep Learning)

### Check GPU
```bash
# Check NVIDIA GPU
nvidia-smi
watch -n 1 nvidia-smi  # Monitor in real-time

# Check CUDA version
nvcc --version

# Check if PyTorch can see GPU
python3 -c "import torch; print(torch.cuda.is_available())"
python3 -c "import torch; print(torch.cuda.device_count())"
```

## Git for Data Science Projects

### Common Workflows
```bash
# Initialize project
git init
git add README.md requirements.txt
git commit -m "Initial commit"

# Ignore large files
echo "*.csv" >> .gitignore
echo "data/" >> .gitignore
echo "models/" >> .gitignore
echo "__pycache__/" >> .gitignore
echo "*.ipynb_checkpoints" >> .gitignore

# Track notebooks (without outputs)
jupyter nbconvert --clear-output --inplace notebook.ipynb
git add notebook.ipynb
```

## Docker for Data Science

### Basic Docker Commands
```bash
# Pull data science images
docker pull jupyter/datascience-notebook
docker pull tensorflow/tensorflow

# Run Jupyter in Docker
docker run -p 8888:8888 jupyter/datascience-notebook

# Mount local directory
docker run -v $(pwd):/home/jovyan/work -p 8888:8888 jupyter/datascience-notebook
```

## Performance & Monitoring

### System Resources
```bash
# Monitor CPU/Memory during training
htop

# Monitor GPU
watch -n 1 nvidia-smi

# Check Python process memory
ps aux | grep python

# Limit CPU cores for process
taskset -c 0-3 python3 script.py
```

## Database Commands

### SQLite
```bash
# Install
sudo apt install sqlite3

# Open database
sqlite3 database.db

# Execute query
sqlite3 database.db "SELECT * FROM table_name;"

# Export to CSV
sqlite3 -header -csv database.db "SELECT * FROM table;" > output.csv
```

### PostgreSQL
```bash
# Install
sudo apt install postgresql postgresql-contrib

# Connect
psql -U username -d database_name

# Backup
pg_dump database_name > backup.sql

# Restore
psql database_name < backup.sql
```

## Useful Aliases for Data Science

```bash
# Add to ~/.bashrc or ~/.bash_aliases
alias jn='jupyter notebook'
alias jl='jupyter lab'
alias py='python3'
alias ipy='ipython'
alias activate='source venv/bin/activate'
alias pipr='pip3 install -r requirements.txt'
alias freeze='pip3 freeze > requirements.txt'
alias nb-clear='jupyter nbconvert --clear-output --inplace'
```

## Complete Setup Script

```bash
#!/bin/bash
# Data Science Environment Setup

# Update system
sudo apt update && sudo apt upgrade -y

# Install Python and essentials
sudo apt install python3 python3-pip python3-venv -y

# Install data science libraries
pip3 install numpy pandas scipy matplotlib seaborn scikit-learn jupyter jupyterlab

# Install additional tools
pip3 install ipython streamlit plotly

# Create project directory
mkdir -p ~/data-science-projects
cd ~/data-science-projects

# Create virtual environment template
python3 -m venv ds-env
source ds-env/bin/activate

echo "Data science environment ready!"
echo "Activate with: source ~/data-science-projects/ds-env/bin/activate"
```

## Quick Start Guide

1. **Setup Environment**:
```bash
python3 -m venv myproject
source myproject/bin/activate
pip install pandas numpy matplotlib jupyter
```

2. **Start Working**:
```bash
jupyter notebook
# or
ipython
```

3. **Save Dependencies**:
```bash
pip freeze > requirements.txt
```

4. **Share Project**:
```bash
git init
echo "venv/" >> .gitignore
git add .
git commit -m "Initial commit"
```

---

**Previous**: [Advanced Commands](03-advanced-commands.md) | **Next**: [Git & GitHub Commands](05-git-github-commands.md)
