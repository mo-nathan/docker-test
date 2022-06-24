# docker-test
Repo for testing Docker/RedCloth bug

The bug is that RedCloth incorrectly truncates strings that contain non-ascii
characters such as ü.  This problem does occurs on Apple M1 systems, but not
on Apple Intel systems.  Your mileage may vary with other hardware that hasn't
been tested (but I would guess it works everywhere except Apple M1 systems).

TL;DR - The following steps should reproduce the error
    ./setup
    docker exec -it rails_test bash
    rails c
    RedCloth.new("Fübar").to_html

Expected results:
    => "<p>Fübar</p>"

Results on Apple M1:
    => "<p>F</p>"
