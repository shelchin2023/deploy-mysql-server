git clone https://github.com/shelchin2023/deploy-mysql-server.git mysql-demo

# 创建环境变量

cd mysql-demo
touch .env
export SECRET_KEY_BASE=$(openssl rand -base64 48)
export MYSQL_ROOT_PASSWORD=$(openssl rand -hex 16)
export MYSQL_PASSWORD=$(openssl rand -hex 16)
echo "MYSQL_ROOT_PASSWORD=$MYSQL_ROOT_PASSWORD" >> .env
echo "MYSQL_PASSWORD=$MYSQL_PASSWORD" >> .env


# 创建 compose override 文件

cat > override.yml << EOF
services:
 mysql:
    environment:
      -MYSQL_ROOT_PASSWORD
      -MYSQL_PASSWORD
EOF
