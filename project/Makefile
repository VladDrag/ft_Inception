all:
	@printf "Launch configuration \n"
	@sudo ./srcs/requirements/wordpress/tools/make_dir.sh
	@sudo docker-compose -f ./srcs/docker-compose.yml --env-file srcs/.env up -d
	@sudo docker exec -i mariadb mysql -u root -prootpass wordpress < srcs/requirements/mariadb/tools/dump.sql

build:
	@printf "Building configuration \n"
	@bash srcs/requirements/wordpress/tools/make_dir.sh
	@sudo docker-compose -f ./srcs/docker-compose.yml --env-file srcs/.env up -d --build
	@sudo docker exec -i mariadb mysql -u root -prootpass wordpress < srcs/requirements/mariadb/tools/dump.sql

down:
	@printf "Stopping configuration \n"
	@sudo docker-compose -f ./srcs/docker-compose.yml --env-file srcs/.env down

re: down
	@printf "Rebuild configuration \n"
	@sudo docker-compose -f ./srcs/docker-compose.yml --env-file srcs/.env up -d --build

fclean:
	@sudo docker exec mariadb mysqldump -u wpuser -pwppass wordpress > ./srcs/requirements/mariadb/tools/dump.sql
	@sudo ./srcs/requirements/tools/clear_docker.sh

.PHONY	: all build down re fclean
