vsftpd-grok-patterns
====================

Logstash configuration and grok patterns for parsing vsftpd logging

Usage
-----

- Install logstash
- Add `50-filter-vsftpd.conf` to `/etc/logstash/conf.d`
- Add `vsftpd.grok` to `/etc/logstash/patterns.d`
- Restart logstash

The included Logstash config file expects the vsftpd log data in the message field, something that works out of the box when you use Logstash's`syslog`input to receive vsftpd logging.

Tests
-----

[![Build Status](https://travis-ci.org/Dh0mp5eur/vsftpd-grok-patterns.svg?branch=master)](https://travis-ci.org/Dh0mp5eur/vsftpd-grok-patterns)

In the `test/` directory, there is a test suite that tries to make sure that no previously supported log line will break because of changing common patterns and such. It also returns results a lot faster than doing `sudo service logstash restart` :-).

The test suite needs the patterns provided by Logstash, you can easily pull these from github by running `git submodule update --init`. To run the test suite, you also need `ruby 1.9` and the `jls-grok` gem. Then simply execute `ruby test/test.rb`.

Adding new test cases can easily be done by creating new yaml files in the test directory. Each file specifies a grok pattern to validate, a sample log line, and a list of expected results.

Also, the example Logstash config file adds some informative tags that aid in finding grok failures and unparsed lines. If you're not interested in those, you can remove all occurrences of `add_tag` and `tag_on_failure` from the config file.

Contributing
------------

I only have access to my own log samples, and my setup does not support or use every feature in vsftpd. If you miss anything, please do a pull request on github. If you're not very well versed in regular expressions, it's also fine to only submit sample unsupported log lines.

License
-------

Everything in this repository is available under the New (3-clause) BSD license.

Acknowledgement
---------------
I use vsftpd (3.0.2), logstash (1.4.2), elasticsearch (1.1.2) and kibana (3.1.3) in order to get everything working.
For writing the grok patterns I depend heavily on [grokdebug](https://grokdebug.herokuapp.com/), and I looked a lot at [antispin's useful logstash grok patterns](http://antisp.in/2014/04/useful-logstash-grok-patterns/).
