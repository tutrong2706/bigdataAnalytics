python3 -m venv btl_env
source btl_env/bin/activate

sudo apt update
sudo apt install openjdk-17-jdk -y
export JAVA_HOME=/usr/lib/jvm/java-17-openjdk-amd64
export PATH=$JAVA_HOME/bin:$PATH

pip install pyspark

sudo apt install python3.10 python3.10-venv python3.10-dev
pip install pandas numpy scikit-learn imbalanced-learn
pip install --upgrade pip

pip install jupyterlab