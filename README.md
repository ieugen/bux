# bux

A money and currency manipulation library for Clojure

[![Build Status](https://secure.travis-ci.org/pelle/bux.png)](http://travis-ci.org/pelle/bux)

## Usage

Add the following to your project.clj

    [bux "0.1.0"]

### Currencies

    (use 'bux.currency)

Create a currency using create-currency:

    (create-currency {:symbol "$", :subunit "Centavo", :name "Argentine Peso", :iso-code "ARS", :iso-numeric "032", 
    :subunit-to-unit 100, :html-entity "&#x20B1;", :symbol-first true, :priority 100})
    => #bux.currency.Currency{:iso-code "ARS", :name "Argentine Peso", :symbol "$", :subunit "Centavo", :subunit-to-unit 100, :symbol-first true, :html-entity "&#x20B1;", :iso-numeric "032", :priority 100}


Define currencies as vars in your current namespace:

    (defcurrency {:symbol "$", :subunit "Centavo", :name "Argentine Peso", :iso-code "ARS", :iso-numeric "032", 
    :subunit-to-unit 100, :html-entity "&#x20B1;", :symbol-first true, :priority 100})
    => #'user/ARS

Load up predefined currencies:

    (use 'bux.currencies)

This adds all current national currencies to the bux.currencies namespace using the ISO code as the symbol.

    USD
    => #bux.currency.Currency{:iso-code "USD", :name "United States Dollar", :symbol "$", :subunit "Cent", :subunit-to-unit 100, :symbol-first true, :html-entity "$", :iso-numeric "840", :priority 1}

Note currency list lifted from [Ruby Money](http://rubymoney.github.com/money/)

### Money

Money is basically clojure numbers representing a currency subunit. So for USD the number would be the amount of cents.

To format it use the currency object as a function

    (USD 123)
    => "$1.23"


Parse strings:

    (->$ USD "$1,123.00")
    => 112300

### Calculations

    (use 'bux.calc)

Percentage:

    (perc 123 10)
    => 12    

With Percentage (can be used for including sales tax, commissions etc.):

    (perc+ 123 10)
    => 135

Percentage discount:

    (perc- 123 10)
    => 111


## License

Copyright (C) 2012 Pelle Braendgaard http://stakeventures.com

Distributed under the Eclipse Public License, the same as Clojure.
