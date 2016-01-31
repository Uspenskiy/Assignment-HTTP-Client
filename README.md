## Модуль #3, Задание 1: Food 2 Fork HTTP API Interface

Целью данного задания явлаеться реальзация источника данных для использывания MVC Model class будушего приложения.

Функциональня цель явлаеться реализация restful API клиента для сервиса `http://food2fork.com/about/api` который возвраешет  JSON данные содержашие рецепт.

### Функциональные требования

1. Реализовать класс который:

    * ишет по ключевым словам
    * передает ключевое слово в `http://food2fork.com/about/api` с использыванием HTTParty API
    * возврашает JSON документ содеражий информацию о рецепте с сервиса http://food2fork.com/about/api

### 

0. Зарегестрироваться ( создать аккаунт) в Food 2 Fork account at `http://food2fork.com/about/api`. Выбрать бесплатны план для получения 500 запросов в день. Когда вы зайдете необходимо вам будет доступен "API Key" на админской странице.

    * определить переменну окружения(FOOD2FORK_KEY) хранашую ваш API Key

1. Скачать и распокавть стартовый набор начальных файлов.

    ```shell
    --- student-start
      |-- .rspec (important hidden file)
      |-- chocolate_recipes.json
      |-- module3_1_assignment.rb
      |-- solution.rb
      `-- spec
          |-- recipe_spec.rb
          `-- spec_helper.rb
    ```
    
    * .rspec - configuration file for unit tests. If you move your files you must take 
      care to also copy this file.
    * module3_lesson1_assignment.rb - contains the starting example.
    Your solution must be placed within this file.
    * spec - this directory contains tests to verify your solution. You should
    not modify anything in this directory
    * chocolate_recipes.json - used for off-line unit testing by rspec tests

2. Установить следуюшие gems для использывания юнитестирования ( rspec ). Может быть некоторые уже установленны.
Последний gem используеться для тестирования HTTP вызовов без использования настояшего сайта `http://food2fork.com/`.

    ```shell
    $ gem install rspec
    $ gem install rspec-its
    $ gem install webmock
    ```

3. Прочитай документацию Food2Fork и HTTParty.

    * HTTParty API документация находиться по адресу `https://github.com/jnunemaker/httparty`
    * Food2Fork описание интерфейса находиться по адресу `http://food2fork.com/about/api`

4. Реализовать Ruby класс с именем `module3_1_assignment.rb`.

5. Запустить rspec тесты и получить отклик. Если вы скопируете/переместите  If you copy/move them,
be sure to include the important .rspec hidden file. All tests will
(obviously) fail until you complete the specified solution.

    ```shell
    $ rspec

    Recipe
      should respond to #for (FAILED - 1)
      Environment variable FOOD2FORK_KEY is set (FAILED - 2)
      default_params[:key] equals Environment variable FOOD2FORK_KEY (FAILED - 3)
      default_params
        example at ./spec/recipe_spec.rb:18 (FAILED - 4)
      base_uri
        example at ./spec/recipe_spec.rb:26 (FAILED - 5)
      Chocolate Search
        example at ./spec/recipe_spec.rb:39 (FAILED - 6)
        size
          example at ./spec/recipe_spec.rb:42 (FAILED - 7)
        sample
          example at ./spec/recipe_spec.rb:45 (FAILED - 8)
        sample
          example at ./spec/recipe_spec.rb:46 (FAILED - 9)
        sample
          example at ./spec/recipe_spec.rb:47 (FAILED - 10)
        sample
          example at ./spec/recipe_spec.rb:48 (FAILED - 11)

    Failures:

      1) Recipe should respond to #for
         Failure/Error: it { is_expected.to respond_to(:for) }
           expected Recipe to respond to :for
         # ./spec/recipe_spec.rb:11:in `block (2 levels) in <top (required)>'

      2) Recipe Environment variable FOOD2FORK_KEY is set
         Failure/Error: expect(ENV["FOOD2FORK_KEY"]).to_not be_nil
           expected: not nil
                got: nil
         # ./spec/recipe_spec.rb:14:in `block (2 levels) in <top (required)>'

      3) Recipe default_params[:key] equals Environment variable FOOD2FORK_KEY
         Failure/Error: expect(subject.default_params[:key]).to eq ENV["FOOD2FORK_KEY"]
         NoMethodError:
           undefined method `default_params' for Recipe:Class
         # ./spec/recipe_spec.rb:22:in `block (2 levels) in <top (required)>'

      4) Recipe default_params
         Failure/Error: its(:default_params) { is_expected.to include :key }
         NoMethodError:
           undefined method `default_params' for Recipe:Class
         # ./spec/recipe_spec.rb:18:in `block (2 levels) in <top (required)>'

      5) Recipe base_uri
         Failure/Error: its(:base_uri) { is_expected.to include "http://food2fork.com/api" }
         NoMethodError:
           undefined method `base_uri' for Recipe:Class
         # ./spec/recipe_spec.rb:26:in `block (2 levels) in <top (required)>'

      6) Recipe Chocolate Search
         Failure/Error: query = Recipe.default_params.merge({"q" => "chocolate"})
         NoMethodError:
           undefined method `default_params' for Recipe:Class
         # ./spec/recipe_spec.rb:31:in `block (3 levels) in <top (required)>'

      7) Recipe Chocolate Search size
         Failure/Error: query = Recipe.default_params.merge({"q" => "chocolate"})
         NoMethodError:
           undefined method `default_params' for Recipe:Class
         # ./spec/recipe_spec.rb:31:in `block (3 levels) in <top (required)>'

      8) Recipe Chocolate Search sample
         Failure/Error: query = Recipe.default_params.merge({"q" => "chocolate"})
         NoMethodError:
           undefined method `default_params' for Recipe:Class
         # ./spec/recipe_spec.rb:31:in `block (3 levels) in <top (required)>'

      9) Recipe Chocolate Search sample
         Failure/Error: query = Recipe.default_params.merge({"q" => "chocolate"})
         NoMethodError:
           undefined method `default_params' for Recipe:Class
         # ./spec/recipe_spec.rb:31:in `block (3 levels) in <top (required)>'

      10) Recipe Chocolate Search sample
          Failure/Error: query = Recipe.default_params.merge({"q" => "chocolate"})
          NoMethodError:
            undefined method `default_params' for Recipe:Class
          # ./spec/recipe_spec.rb:31:in `block (3 levels) in <top (required)>'

      11) Recipe Chocolate Search sample
          Failure/Error: query = Recipe.default_params.merge({"q" => "chocolate"})
          NoMethodError:
            undefined method `default_params' for Recipe:Class
          # ./spec/recipe_spec.rb:31:in `block (3 levels) in <top (required)>'

    Finished in 0.01817 seconds (files took 0.39671 seconds to load)
    11 examples, 11 failures

    Failed examples:

    rspec ./spec/recipe_spec.rb:11 # Recipe should respond to #for
    rspec ./spec/recipe_spec.rb:13 # Recipe Environment variable FOOD2FORK_KEY is set
    rspec ./spec/recipe_spec.rb:21 # Recipe default_params[:key] equals Environment variable FOOD2FORK_KEY
    rspec ./spec/recipe_spec.rb:18 # Recipe default_params
    rspec ./spec/recipe_spec.rb:26 # Recipe base_uri
    rspec ./spec/recipe_spec.rb:39 # Recipe Chocolate Search
    rspec ./spec/recipe_spec.rb:42 # Recipe Chocolate Search size
    rspec ./spec/recipe_spec.rb:45 # Recipe Chocolate Search sample
    rspec ./spec/recipe_spec.rb:46 # Recipe Chocolate Search sample
    rspec ./spec/recipe_spec.rb:47 # Recipe Chocolate Search sample
    rspec ./spec/recipe_spec.rb:48 # Recipe Chocolate Search sample
    ```

6. Запустите `solution.rb` Ruby скрипт и получите вызов.

    ```ruby
    require_relative "module3_1_assignment"

    puts Recipe.for("chocolate")
    ```

### Технические требования

1. Определить переменную окружения FOOD2FORK_KEY которая хронит ваш API Key от `food2fork.com`.

2. Реализовать `Recipe` класс который реализует the HTTP API к `http://food2fork.com/about/api`.
Юнитесты  The unit tests will expect a class by that exact name.

3. Класс `Recipe` должен

    * реализовыван в файле `module3_1_assignment.rb`. Фаил юни тестов должен иметь тоже имя.
    * импортировать HTTParty миксин
    * определен base_uri для использывания `http://food2fork.com/api`
    * определен значения по умлочанию параметров запросов `key` для всех HTTP GET
    запросы чьи значения равны переменной окружения FOOD2FORK_KEY.
    * указать тебуемый формат `json`
    * указать все выше описываемое Ruby синтаксисом

4.  Класс `Recipe` должен иметь метод `for` который 

    * Принимает ключевое слово для поискового запроса
    * Отправлять HTTP GET запросы с использывание gem-a HTTParty
    * HTTP GET запросы должны иметь "q=ключевое слово" query argument and query "/search" route
    * returns the JSON payload document supplied in the `recipes` element of the hash returned by HTTParty

### Self Grading/Feedback

Some unit tests have been provided in the bootstrap files that can be
used to evaluate your solution. They must be run from the same directory
as your solution.

```shell
$ rspec

Recipe
  should respond to #for
  Environment variable FOOD2FORK_KEY is set
  default_params[:key] equals Environment variable FOOD2FORK_KEY
  default_params
    should include :key
  base_uri
    should include "http://food2fork.com/api"
  Chocolate Search
    should be a kind of Array
    size
      should eq 30
    sample
      should have key "title"
    sample
      should have key "f2f_url"
    sample
      should have key "social_rank"
    sample
      should have key "image_url"

Finished in 0.02369 seconds (files took 0.40009 seconds to load)
```

A client script (`solution.rb`) is also provided in the bootstrap
and can be used to issue a sample client request.


```ruby
$ ruby solution.rb 
{"publisher"=>"BBC Good Food", "f2f_url"=>"http://food2fork.com/view/9089e3", 
"title"=>"Cookie Monster cupcakes",
"source_url"=>"http://www.bbcgoodfood.com/recipes/873655/cookie-monster-cupcakes", 
"recipe_id"=>"9089e3", "image_url"=>"http://static.food2fork.com/604133_mediumd392.jpg",
"social_rank"=>100.0, "publisher_url"=>"http://www.bbcgoodfood.com"}
...
{"publisher"=>"Elana's Pantry", "f2f_url"=>"http://food2fork.com/view/22d607", 
"title"=>"Brownies", 
"source_url"=>"http://www.elanaspantry.com/brownies/", 
"recipe_id"=>"22d607", "image_url"=>"http://static.food2fork.com/dsc_8204brownies7a41.jpg", 
"social_rank"=>99.99999999990415, "publisher_url"=>"http://www.elanaspantry.com"}
```

### 

 There is no submission required for this assignment but the 
implementation will be part of a follow-on assignment so 
please complete this to the requirements of the unit test.

Your final directory contents should look as follows:

```shell
|-- module3_1_assignment.rb
|-- chocolate_recipes.json
|-- solution.rb
|-- .rspec (important hidden file)
`-- spec
    |-- recipe_spec.rb
    `-- spec_helper.rb
```

#### Updated: 2015-09-22
