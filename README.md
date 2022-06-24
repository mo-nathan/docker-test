# docker-test
Repo for testing Docker/RedCloth bug

The bug is that RedCloth incorrectly truncates strings that contain non-ascii
characters such as ü.  This problem does occurs on Apple M1 systems, but not
on Apple Intel systems.  Your mileage may vary with other hardware that hasn't
been tested (but I would guess it works everywhere except Apple M1 systems).

## TL;DR - The following steps should reproduce the error
```
./setup
docker exec -it rails_test bash
rails c
RedCloth.new("Fübar").to_html
```

Expected results: `=> "<p>Fübar</p>"`

Results on Apple M1: `=> "<p>F</p>"`

## More Details
The `setup` script checks out the sister repo
https://github.com/mo-nathan/rails-test which is an automatically
generated Rails app (`rails new rails-test` with Rails version 6.1.6))
that then has the RedCloth gem added to the Gemfile.  A Dockerfile is
added to use the standard ruby:2.7.6 docker image to run that app.
The versions of Ruby and Rails is based on the actually app I am
trying to get to work.  However, the same issue occurs with Ruby 3.1.2
and Rails 7.0.3 (see branch rails-7.0.3).

The problem also goes away if your remove Docker from the equation and
just run `rails c` directly on the Apple M1 system.

macOS Monterey Version 12.4.
