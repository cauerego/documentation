---
title: Continuous Integration Solutions on Pantheon
description: Run automated unit and integration tests with Terminus and Drupal SimpleTest.
category:
  - going-live
  - developing
keywords: continuous integration, tests, testing, terminus, drupal,
---
Continuous Integration (CI) is a method of running automated unit and integration tests to apply quality control. Pantheon doesn't provide or host tools for continuous integration, but many tools and techniques are compatible with Pantheon. If you have a particular use case or technique that you'd like to highlight, let us know by opening a support ticket.

## Terminus Command-Line Interface

[Terminus](/docs/articles/local/terminus-the-pantheon-command-line-interface/) is a Drush-based command-line interface (CLI) in the Pantheon core API. Most operations available through the Pantheon Dashboard can be performed with Terminus, including:

- Site creation
- [Multidev environment](/docs/articles/sites/multidev) creation and removal
- Content cloning
- Code pushes

You can use Terminus for scripting many operations. For example, a post-commit hook can trigger Jenkins to create a Multidev environment with the latest code on master and the content from Live, then run automated browser tests using [Selenium](http://www.seleniumhq.org/).

## Drupal SimpleTest

[SimpleTest](https://drupal.org/project/simpletest) is a testing framework based on the [SimpleTest PHP library](http://simpletest.sourceforge.net/) that is included with Drupal core. If you are creating a custom web application, you should consider including SimpleTests of your module functionality.

After enabling the SimpleTest module, you can use Drush to remotely execute SimpleTest on your Pantheon site. For example, if you want to execute the UserSaveTestCase test and generate XML output into a writeable directory, use the following command:

    SITE_NAME=yoursitename
    ENV=dev
    drush @pantheon.$SITE_NAME.$ENV test-run -l http://$ENV-$SITE_NAME.pantheon.io/ UserSaveTestCase --xml='sites/default/files'

The end result is written to http://dev-yoursitename.pantheon.io/sites/default/files/UserSaveTestCase.xml

## Integration Bot

We recommend creating a bot user account that will handle the tasks or jobs by an external continuous intergration service rather a standard user account.

- Add the bot to select projects
- Manage separate SSH Keys for CI

## Known Limitations

At this time, Pantheon does not provide or support:

- [Webhooks](http://en.wikipedia.org/wiki/Webhook)
- [Git hooks](http://git-scm.com/book/en/Customizing-Git-Git-Hooks)
- Running [Jenkins](http://jenkins-ci.org/) or other Continuous Integration software on our servers. You'll need to self-host or use a hosted CI solution. [Compare solutions here](https://en.wikipedia.org/wiki/Comparison_of_continuous_integration_software).
- Shell access
- [PHPUnit](https://github.com/sebastianbergmann/phpunit/) Unit Testing PHP Framework: You can still write tests and include them in your code, but you'll need to run them on a CI server, not Pantheon.
