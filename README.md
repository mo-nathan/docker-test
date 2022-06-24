# docker-test
Repo for testing Docker/RedCloth interaction

TL;DR - The following steps should reproduce the error
    ./setup
    docker exec -it rails_test bash
    rails c
    RedCloth.new("Fübar").to_html
