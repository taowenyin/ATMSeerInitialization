# ATMSeerInitialization

[ATMSeer](https://github.com/HDI-Project/ATMSeer)安装方法

[传统安装方法](./Normal.md)

> 此安装方法，截止到2019-08-20，ATM的版本为0.10

#### 1、vagrant init ubuntu/xeni

#### 2、vagrant up

#### 3、vagrant ssh

#### 4、sudo cp /etc/apt/sources.list /etc/apt/sources.list.bk

#### 5、sudo sed -i 's/archive.ubuntu.com/mirrors.ustc.edu.cn/g' /etc/apt/sources.list

#### 6、sudo apt-get update

#### 7、sudo add-apt-repository ppa:apt-fast/stable

#### 8、sudo apt-get update

#### 9、sudo apt-get install apt-fast

#### 10、sudo apt-get upgrade

#### 11、sudo add-apt-repository ppa:jonathonf/python-3.6

#### 12、sudo apt-get update

#### 13、sudo apt-get install python3.6 python3.6-dev python3.6-gdbm

#### 14、sudo update-alternatives --install /usr/bin/python python /usr/bin/python3.6 1

#### 15、sudo update-alternatives --install /usr/bin/python3 python3 /usr/bin/python3.6 1

#### 16、curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py

#### 17、python get-pip.py --user

#### 18、pip config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple

#### 19、sudo apt-get install gcc g++ build-essential

#### 20、curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.34.0/install.sh | bash

#### 21、source .bashrc

#### 22、nvm install node

#### 23、npm config set registry https://registry.npm.taobao.org

#### 24、wget https://dev.mysql.com/get/mysql-apt-config_0.8.13-1_all.deb

#### 25、sudo dpkg -i mysql-apt-config_0.8.13-1_all.deb

#### 26、sudo apt-get update

#### 27、sudo apt-get -y install mysql-server sqlite3 libmysqlclient-dev

#### 28、pip install virtualenv --user

#### 29、cd /vagrant/

#### 30、mkdir ATM

#### 31、cd ATM

#### 32、virtualenv -p $(which python3.6) venv

#### 33、source venv/bin/activate

#### 34、git clone https://github.com/HDI-Project/ATMSeer.git

#### 35、tar zxvf ATM-@9dfe5d9.tar.gz -C ATMSeer/lib/

#### 36、cd ATMSeer

#### 37、pip install -r lib/atm/requirements.txt

#### 38、pip install lib/atm/

#### 39、pip install -r server/requirements.txt

#### 40、pip uninstall scikit_learn

#### 41、pip install scikit_learn==0.19.2

#### 42、pip uninstall pandas

#### 43、pip install pandas==0.24.2

#### 44、cd lib/atm/

#### 45、python setup.py install

#### 46、cd ../..

#### 47、npm install

#### 48、分两个窗口，一个窗口运行./startserver.sh，另一个窗口运行npm start
