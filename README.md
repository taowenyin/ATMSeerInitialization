# ATMSeerInitialization

[ATMSeer](https://github.com/HDI-Project/ATMSeer)安装方法

> 此安装方法，截止到2019-08-20，ATM的版本为0.10

### 1、vagrant init ubuntu/xeni

### 2、vagrant up

### 3、vagrant ssh

### 4、sudo cp /etc/apt/sources.list /etc/apt/sources.list.bk

### 5、sudo sed -i 's/archive.ubuntu.com/mirrors.ustc.edu.cn/g' /etc/apt/sources.list

### 6、sudo apt-get update

### 7、sudo apt-get upgrade

### 8、sudo add-apt-repository ppa:jonathonf/python-3.6

### 9、sudo apt-get update

### 10、sudo apt-get install python3.6 python3.6-dev python3.6-gdbm

### 11、sudo update-alternatives --install /usr/bin/python python /usr/bin/python3.6 1

### 12、sudo update-alternatives --install /usr/bin/python3 python3 /usr/bin/python3.6 1

### 13、curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py

### 14、python get-pip.py --user

### 15、pip config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple

### 16、sudo apt-get install gcc g++ build-essential

### 17、curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.34.0/install.sh | bash

### 18、source .bashrc

### 19、nvm install node

### 20、npm config set registry https://registry.npm.taobao.org

### 21、wget https://dev.mysql.com/get/mysql-apt-config_0.8.13-1_all.deb

### 22、sudo dpkg -i mysql-apt-config_0.8.13-1_all.deb

### 23、sudo apt-get update

### 24、sudo apt-get -y install mysql-server sqlite3 libmysqlclient-dev

### 25、pip install virtualenv --user

### 26、cd /vagrant/

### 27、mkdir ATM

### 28、cd ATM

### 29、virtualenv -p $(which python3.6) venv

### 30、source venv/bin/activate

### 31、git clone https://github.com/HDI-Project/ATMSeer.git

### 32、tar zxvf ATM-@9dfe5d9.tar.gz -C ATMSeer/lib/

### 33、cd ATMSeer

### 34、pip install -r lib/atm/requirements.txt

### 35、pip install lib/atm/

### 36、pip install -r server/requirements.txt

### 37、pip uninstall scikit_learn

### 38、pip install scikit_learn==0.19.2

### 39、pip uninstall pandas

### 40、pip install pandas==0.24.2

### 41、cd lib/atm/

### 42、python setup.py install

### 43、cd ../..

### 44、npm install

### 45、分两个窗口，一个窗口运行./startserver.sh，另一个窗口运行npm start
