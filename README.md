Your task is to write a script that prints a list of test cases that will be run by our existing testing infrastructure.

At [GeoIP2 Precision Web Services/MaxMind Developer Site](https://dev.maxmind.com/geoip/geoip2/web-services/), under the section `IP Address`, you will find a description of the IP address format accepted by GeoIP2 web services.

As part of the test suite we maintain for the GeoIP2 Precision Web Services, we send IP addresses to a test server, and check it responds correctly. Part of the test plan requires we test the parsing of IP addresses. From the GeoIP2 link above:

    The IP address can be either an IPv4 or an IPv6 address. IPv4 addresses should
    be passed in the standard dotted quad form, for example 1.2.3.4. IPv6 addresses
    should be passed as strings as well. We recommend using the canonical form as
    described in RFC 5952, for example 2001:db8::1:0:0:1, but we will handle any
    valid IPv6 string representation.

    You can also use the string me as the IP address. In this case, the record for
    the IP address you are querying from will be returned. This is useful when your
    application does not have easy access to its public IP address, e.g., when the
    system making the query is behind a NAT.

**Your task** is to help us test the GeoIP2 fault models that relate to _parsing IP addresses_. You will write a test plan and a script that prints out test cases according to this plan.

1. Write a short test plan in a `README` file. Select one or more of the fault models possible with this feature. Describe  in 1-4 short paragraphs:

    * The fault model you selected
    * The types of IP addresses you would use to test this fault model
    * Specify why you selected these types of IP addresses to test this fault model

1. Write a script implementing the plan.

    * Your script should print test cases to the terminal, where each test case is an IP address and a Boolean describing expected result of the service under test

    * It should accept exactly one command line argument, with two possible values:
        1. quick - which causes your script to print 10 test cases, or
        1. comprehensive - which causes your script to print 100 test cases.

    * Each test case you should show is a single line, in CSV format, with two fields:
        1. The first is the IP address you want to test
        1. The second is a 1 or a 0. A 1 is defined as this IP address should be OK, and 0 as: this IP address should throw an error.

Example output line from your script where we predict an IP address is valid:

```
51.64.74.79,1
```

And another where we expect an error due to IP address parse failure:

```
192.:).0.138,0
```


Our existing testing infrastructure will read the output of this script, construct HTTP requests for each IP address, and send the requests to some implementation. It will then assert your predictions are correct: all and only invalid addresses fail.

Please note:

* We don't care much about coverage- rather we do like to see intense focus on the challenges of a tiny fault model, and the creative testing required to meet them.
* **Please write your example in Perl, Python, Ruby, JavaScript, PHP, or Go. If you want to use a different language please contact us first.** If you use any third party libraries, you must deliver the end result in a way that allows us to run the code on a standard Ubuntu Trusty or Xenial system. That means either packaging up all of your dependencies or giving us very clear instructions on how to install them. Unless the language you choose is Perl or Go, assume that we do not know anything about the package management tools for that language! We will run your code to look at the output, as well as looking at the code itself.
* Your script should only print test cases. It should _not_ do any actual testing

Please complete the assignment and share your script and README.
