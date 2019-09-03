#### 1、vagrant init ubuntu/xeni

#### 2、vagrant up

#### 3、vagrant ssh

#### 4、sudo cp /etc/apt/sources.list /etc/apt/sources.list.bk

#### 5、sudo sed -i 's/archive.ubuntu.com/mirrors.ustc.edu.cn/g' /etc/apt/sources.list

#### 6、sudo apt-get update

#### 7、sudo add-apt-repository ppa:apt-fast/stable

#### 8、sudo apt-get update

#### 9、sudo apt-get install apt-fast

#### 10、sudo apt-fast upgrade

#### 11、sudo add-apt-repository ppa:jonathonf/python-3.6

#### 12、sudo apt-fast update

#### 13、sudo apt-fast install python3.6 python3.6-dev python3.6-gdbm

#### 14、sudo update-alternatives --install /usr/bin/python python /usr/bin/python3.6 1

#### 15、sudo update-alternatives --install /usr/bin/python3 python3 /usr/bin/python3.6 1

#### 16、curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py

#### 17、python get-pip.py --user

#### 18、pip config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple

#### 19、sudo apt-fast install gcc g++ build-essential

#### 20、curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.34.0/install.sh | bash

#### 21、source .bashrc

#### 22、nvm install node

#### 23、npm config set registry https://registry.npm.taobao.org

#### 24、wget https://dev.mysql.com/get/mysql-apt-config_0.8.13-1_all.deb

#### 25、sudo dpkg -i mysql-apt-config_0.8.13-1_all.deb

#### 26、sudo apt-fast update

#### 27、sudo apt-fast -y install mysql-server sqlite3 libmysqlclient-dev

#### 28、pip install virtualenv --user

#### 29、cd /vagrant/

#### 30、mkdir ATM

#### 31、cd ATM

#### 32、virtualenv -p $(which python3.6) atm-venv

#### 33、source atm-venv/bin/activate

#### 34、pip install atm

#### 35、pip install Flask-Cors

#### 36、pip install requests

#### 37、git clone https://github.com/HDI-Project/ATMSeer.git

#### 38、pip install -r ATMSeer/server/requirements.txt

#### 39、npm install

#### 40、分两个窗口，一个窗口运行./startserver.sh，另一个窗口运行npm start
