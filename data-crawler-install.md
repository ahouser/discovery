---

copyright:
  years: 2015, 2018, 2019
lastupdated: "2019-01-28"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:note: .note}
{:pre: .pre}
{:important: .important}
{:deprecated: .deprecated}
{:codeblock: .codeblock}
{:screen: .screen}
{:download: .download}
{:hide-dashboard: .hide-dashboard}
{:apikey: data-credential-placeholder='apikey'} 
{:url: data-credential-placeholder='url'}
{:curl: #curl .ph data-hd-programlang='curl'}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:ruby: .ph data-hd-programlang='ruby'}
{:swift: .ph data-hd-programlang='swift'}
{:go: .ph data-hd-programlang='go'}

# Downloading and installing the Data Crawler
{: #downloading-and-installing-the-data-crawler}

The Data Crawler collects the raw data that is eventually used to form search results for the {{site.data.keyword.discoveryshort}} service. When crawling data repositories, the crawler downloads documents and metadata, starting from a user-specified seed URL. The crawler discovers documents in a hierarchy, or otherwise linked from the seed URL, and enqueues these for retrieval.
{: shortdesc}

The Data Crawler should only be used to crawl file shares or databases, in all other cases you should use the appropriate {{site.data.keyword.discoveryshort}} connector. See [Connecting to data sources](/docs/services/discovery/connect.html) for details. Assistance is no longer provided for the Data Crawler if you are using it with a data source supported by the {{site.data.keyword.discoveryshort}} connectors.
{: important}

## Prerequisites
{: #dc-prerequisites}

-   Java Runtime Environment version 8 or higher

    Your `JAVA_HOME` environment variable must be set correctly, or not be set at all, in order to run the Crawler.
    {: tip}
-   Red Hat Enterprise Linux 6 or 7, or Ubuntu Linux 15 or 16. For optimal performance, the Data Crawler should run on its own instance of Linux, whether it is a virtual machine, a container, or hardware.

-   Minimum 2 GB RAM on the Linux system

## Download and install the Data Crawler
{: #dc-download-install}

1.  Open a browser and log into your [{{site.data.keyword.Bluemix}} account ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://{DomainName}/){: new_window}.

1.  From your {{site.data.keyword.Bluemix_notm}} Dashboard, select the {{site.data.keyword.discoveryshort}} service you previously created.

1.  In the **Automate the upload of content to the Discovery service** section, click the appropriate link to download the Data Crawler for Linux in DEB, RPM, and ZIP formats.

1.  Verify that you are running Java Runtime Environment version 8 or higher. Run the command `java -version`, and look for **1.8**. If you are running something earlier than **1.8**, you need to upgrade Java by installing the Java Developer Kit (JDK) 8 from your package management system, from the [IBM JDK ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/developerworks/java/jdk/){: new_window} website, or from [java.com ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://www.java.com){: new_window}.

    Your `JAVA_HOME` environment variable must be set correctly, or not be set at all, in order to run the Crawler.
    {: tip}

1.  As an administrator, use the appropriate commands to install the archive file that you downloaded:

    -   On systems such as Red Hat and CentOS that use rpm packages, use a command such as the following: `rpm -i /full/path/to/rpm/package/rpm-file-name`
    -   On systems such as Ubuntu and Debian that use deb packages, use a command such as the following: `dpkg -i /full/path/to/deb/package/deb-file-name`
    -   The Crawler scripts are installed into `{installation_directory}/bin`; for example, `/opt/ibm/crawler/bin`. Ensure that `{installation_directory}/bin` is in your `PATH` environment variable for the Crawler commands to work correctly.

    Crawler scripts are also installed to `/usr/local/bin`, so this can be added to your `PATH` environment variable as well.
    {: tip}
1.  Create your working directory by copying the contents of the `{installation_directory}/share/examples/config` directory to a working directory on your system, for example `/home/config`.

    **Warning:** Do not modify the provided configuration example files directly. Copy and then edit them. If you edit the example files in-place, your configuration may be overwritten when upgrading the Data Crawler, or may be removed when uninstalling it.

    **Note:** References in the rest of this guide to files in the `config` directory, such as `config/crawler.conf`, refer to that file in your working directory, and NOT in the installed `{installation_directory}/share/examples/config` directory.

1.  You are now ready to [configure the Data Crawler to connect to your repository](/docs/services/discovery/data-crawler-seeds.html)

## Data Crawler structure
{: #dc-structure}

The Data Crawler download places the following folders on your system:

-   `doc` - Contains files with copyright and licensing information.
-   `bin` - Script files for running the crawler.
-   `connectorFramework` - The files in this directory are what allow you to talk to your data, whether internal data within the enterprise, or external data on the web or in the cloud.
-   `lib` - Library files used by the crawler.
-   `share`
    -   `doc` - Provides both HTML and Markdown-formatted documentation files.
    -   `examples/config` - Files that let you tell the crawler which data to use for its crawl, where to send your collection of crawled data once the crawl has been completed, and other crawl management options.
    -   `man` - In-product manual page crawler documentation.

## Known limitations in this release
{: #dc-limitations}

-   The Data Crawler may hang when running the Filesystem connector with an invalid or missing URL.
-   Configure the `urls_to_filter` value in the `crawler.conf` file, such that all the whitelist URLs or RegExes are included in a single RegEx expression. See [Configuring crawl options](/docs/services/discovery/data-crawler-discovery.html#configuring-crawl-options) for more information.
-   The path to the configuration file passed in the `--config -c` option must be a qualified path. That is, it must be in the relative formats `config/crawler.conf` or `./crawler.conf`, or absolute path `/path/to/config/crawler.conf`. Specifying just `crawler.conf` is only possible if the `orchestration_service.conf` file is in-lined instead of referenced using `include` in the `crawler.conf` file.
