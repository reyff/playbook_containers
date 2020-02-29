---
  - hosts: exemplo
    remote_user: analista
    become: yes
    tasks:
      - name: "Executa o container MySQL"
        docker_container:
          name: banco
          image: mysql:5.6
          env:
            MYSQL_ROOT_PASSWORD: senha123
      - name: "Executa o container WordPress"
        docker_container:
          name: wordpress
          image: wordpress
          links:
            - "banco:mysql"
          ports:
            - "80:80"
