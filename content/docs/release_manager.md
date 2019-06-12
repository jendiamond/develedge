---
title: "Release Manager Notes"
date: 2019-05-11T21:38:49-07:00
draft: true
---

## Docker Setup for Californica & Ursus

Skip to content
 
Search or jump to…

Pull requests
Issues
Marketplace
Explore
 
@jendiamond 
11
3 0 UCLALibrary/amalgamated-samvera
 Code  Issues 58  Pull requests 1  Projects 0  Wiki  Insights  Settings
Editing Docker Setup for Californica & Ursus
 
Docker Setup for Californica & Ursus
 
    
Edit mode:  
## Californica in Docker
<details><summary>FOLLOW THESE DIRECTIONS TO GET IT SET UP</summary>

#### 1. Clone the repo from GitHub and change directories into the repo

$ `git clone git@github.com:UCLALibrary/californica.git`  
$ `cd californica`

#### 2. Bring up the development environment:

$ `docker-compose up`

#### 3. Provision the database
The first time you create the environment, you'll also need to provision the databases. 
 
>##### Open another tab in your terminal be sure you are in the `californica` directory.  
>To get into the root run:
>
>$ `docker-compose run web bash`  
> 
>##### Now your terminal should look like something this: `root@2b6bd2c19a8a:/californica#`

##### Provision the database  
root@2b6bd2c19a8a:/californica#$ `bundle exec rake db:setup`  

#### 4. Ingest some content  
root@2b6bd2c19a8a:/californica# `bundle exec rake californica:ingest:ladnn_sample`  

You can also run `rake californica:ingest:connell_sample` to get more records and have two collections

*To see all rake options run `rake -T`*

#### If this succeeds without error, you've successfully created your Californica environment and loaded some sample records.

To access some of the services that you'll need, try finding them at the following locations:

- Californica -> http://localhost:3000/
- Fedora -> http://localhost:8080/fcrepo/rest
- Solr -> http://localhost:8983/solr/#/

### Default admin user

A default admin user is created for you, with the e-mail address of admin@example.com, and a password of 'password' This password can and should be set by way of a dot-env variable ADMIN_PASSWORD. See the .env.sample file for an example.

### Creating a new admin user

First, create the user via the UI, or have them self-register.

Then, on the rails console:

```ruby
u = User.find_by_user_key('example@library.ucla.edu')
admin = Role.find_by_name('admin')
admin.users << u
admin.save
u.admin?
  => true
```

If `u.admin?` returns `true` then you know it worked as expected.

See also the [Making Admin Users in Hyrax Guide](https://github.com/samvera/hyrax/wiki/Making-Admin-Users-in-Hyrax).
</details>

---

## Ursus in Docker 2 ways
### Prerequisites
+ [Docker](https://docs.docker.com/install) 
+ [Docker Compose](https://docs.docker.com/compose/install/)  

## 1. Ursus with its own mocked Californica
Run this version of Ursus on its own

+ This developer environment comes pre-populated with data from [Californica-test](https://californica-test.library.ucla.edu)

<details><summary>FOLLOW THESE DIRECTIONS TO GET IT SET UP</summary>

#### 1. Clone the repo from GitHub and change directories into the repo
$ `git clone git@github.com:UCLALibrary/ursus.git`  
$ `cd ursus`  

#### 2. Bring up the development environment:
$ `docker-compose up`  

#### 3. Provision the databases
$ `docker-compose run web bundle exec rake db:setup`  

Ursus should now be running on [port 3003](http://localhost:3003).

The data you're viewing is coming from a solr instance, preloaded with data from [Californica-test]  
(https://californica-test.library.ucla.edu), and should not need to be changed in most cases,  
since Ursus is a discovery interface only.  
You can view the solr console on [port 8983](http://localhost:8983).

### Running the Test Suite

1. Connect to a shell *inside* the container with `docker-compose run web bash`
1. Run `bundle exec rspec spec`
</details>

---

## 2. Ursus connected to the Californica above
#### Running Ursus with/against a local version of Californica
To run this version you must start Californica first.
+ Sometimes you will need to develop in an environment where Ursus and Californica are sharing the same Solr data. 
+ In order to use data from californica, you will need to run our management app Californica alongside Ursus. The file `docker-compose-with-californica.yml` is set up to allow this.

<details><summary>FOLLOW THESE DIRECTIONS TO GET IT SET UP</summary>

1. Get your Californica environment running
[Follow the Californica instructions to get a local instance of Californica running on `port 3000`](https://github.com/UCLALibrary/californica#getting-started)

2. Get your Ursus environment running
    + Spin up your environment and start the app:
        + `docker-compose -f docker-compose-with-californica.yml up`

    + Run the database migration
        + `docker-compose -f docker-compose-with-californica.yml run web bundle exec rake db:setup`

    **Note:** If you get a database error make sure that you are running californica as outlined above (1. Get your Californica environment running)
    ```
    Mysql2::Error::ConnectionError
    Unknown MySQL server host 'db' (-2)
    ```
3. You will have to explicitly specify the alternate `docker-compose` file **every time** you run a `docker-compose` command  
    For example:   
    + Open a shell inside a container  
        `docker-compose -f docker-compose-with-californica.yml run web bash`
    + Run the test suite  
        `docker-compose -f docker-compose-with-californica.yml run web bundle exec rspec spec`

- Ursus -> http://localhost:3003/
- Californica -> http://localhost:3000/
- Fedora -> http://localhost:8080/fcrepo/rest
- Solr -> http://localhost:8983/solr/#/

---

# Running rails commands natively

It is possible to run rails natively against backing services running in docker. Personally, [I](https://github.com/andrewbenedictwallace/) run the rails server in docker but like to run tests and rake commands natively. This has the side benefit of maintaining a copy of Ursus' various dependency libraries in a place where a text editor can find them (they're not very good at digging through docker containers).

[I](https://github.com/andrewbenedictwallace/) haven't worked out consistent instructions for doing this yet, however. Here's a rough outline:

1. Install the proper version of ruby with rvm, rbenv, or similar.
1. Change `config/solr.yml` and `config/blacklight.yml` to point to `http://localhost:8983/solr/calursus` by default.
1. Point `config/database.yml` to `http://127.0.0.1:3306` by default. It's important to *not* use `localhost` here, because that would make the mysql client try to connect via a socket, which doesn't work with docker.
1. Run `bundle install`
</details>
