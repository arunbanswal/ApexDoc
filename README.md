### This project and repository are no longer maintained by Salesforce.org
This version is maintained by Arun :-)

ApexDoc
=======

ApexDoc is a java app that you can use to document your Salesforce Apex classes. You tell ApexDoc where your class files are, and it will generate a set of static HTML pages that fully document each class, including its properties and methods. Each static HTML page will include an expandable menu on its left hand side, that shows a 2-level tree structure of all of your classes. Command line parameters allow you to control many aspects of ApexDoc, such as providing your own banner HTML for the pages to use.
## New in this branch
Classes and/or methods can be marked as *deprecated*; you can also provide a description of what to use instead.  
Methods can use the *exception*; add as many lines as needed to indicate exceptions a method might throw.

## Credits
ApexDoc was originally created by Aslam Bari (http://techsahre.blogspot.com/2011/01/apexdoc-salesforce-code-documentation.html). It was then taken and extended by David Habib, at Groundwire, in 2011. It has subsequently been enhanced by David Habib of the Salesforce Foundation in late 2014 for use with Nonprofit Success Pack (https://github.com/SalesforceFoundation/Cumulus). We are unable to offer direct support of reported issues or incorporate enhancement requests at this time, however pull requests are welcome.

## Command Line Parameters
| parameter | description |
|-------------------------- | ---------------------|
| -s *source_directory* | The folder location which contains your apex .cls classes.|
| -t *target_directory* | The folder location where documentation will be generated to.|
| -g *source_url* | A URL where the source is hosted (so ApexDoc can provide links to your source). Optional.|
| -h *home_page* | The full path to an html file that contains the contents for the home page's content area. Optional.|
| -a *banner_page* | The full path to an html file that contains the content for the banner section of each generated page. Optional.|
| -p *scope* | A semicolon separated list of scopes to document. Defaults to 'global;public;webService'. Optional.|

## Usage
Copy apexdoc.jar file to your local machine, somewhere on your path. Each release tag in gitHub has the matching apexdoc.jar attached to it. Make sure that java is on your path. Invoke ApexDoc like this example:
```
java -jar apexdoc.jar
    -s '/Users/dhabib/Workspaces/Force.com IDE/Cumulus3/src/classes'
    -t '/Users/dhabib/Dropbox/Cumulus/ApexDoc'
    -p 'global;public;private;testmethod;webService'
    -h '/Users/dhabib/Dropbox/Cumulus/ApexDoc/homepage.htm'
    -a '/Users/dhabib/Dropbox/Cumulus/ApexDoc/projectheader.htm'
    -g 'http://github.com/SalesforceFoundation/Cumulus/blob/dev/src/classes/'
```

## Documenting Class Files
ApexDoc scans each class file, and looks for comment blocks with special keywords to identify the documentation to include for a given class, property, or method.  The comment blocks must always begin with /** (or additional *'s) and can cover multiple lines.  Each line must start with * (or whitespace and then *).  The comment block ends with */. Special tokens are called out with @token.
### Class Comments
Located in the lines above the class declaration. The special tokens are all optional.

| token | description |
|-------|-------------|
| @author | the author of the class |
| @date | the date the class was first implemented |
| @group | a group to display this class under, in the menu hierarchy|
| @group-content | a relative path to a static html file that provides content about the group|
| @description | one or more lines that provide an overview of the class|
| @deprecated | indicates class should no longer be used; message should indicate replacement |

Example
```
/**
* @author Salesforce.com Foundation
* @date 2014
*
* @group Accounts
* @group-content ../../ApexDocContent/Accounts.htm
*
* @description Trigger Handler on Accounts that handles ensuring the correct system flags are set on
* our special accounts (Household, One-to-One), and also detects changes on Household Account that requires
* name updating.
*/
public with sharing class ACCT_Accounts_TDTM extends TDTM_Runnable {
```

### Property Comments
Located in the lines above a property. The special tokens are all optional.

| token | description |
|-------|-------------|
| @description | one or more lines that describe the property|

Example
```
    /*******************************************************************************************************
    * @description specifies whether state and country picklists are enabled in this org.
    * returns true if enabled.
    */
    public static Boolean isStateCountryPicklistsEnabled {
        get {
```

### Method Comments
In order for ApexDoc to identify class methods, the method line must contain an explicit scope (global, public, private, testMethod, webService).  The comment block is located in the lines above a method.  The special tokens are all optional.

| token | description |
|-------|-------------|
| @description | one or more lines that provide an overview of the method|
| @param *param name* | a description of what the parameter does|
| @return | a description of the return value from the method|
| @deprecated | indicates method should no longer be used; message should indicate replacement |
| @exception | a description of an Exception that might be thrown |
| @example | Example code usage. This will be wrapped in <code> tags to preserve whitespace|
Example
```
    /*******************************************************************************************************
    * @description Returns field describe data
    * @param objectName the name of the object to look up
    * @param fieldName the name of the field to look up
    * @return the describe field result for the given field
    * @example
    * Account a = new Account();
    */
    public static Schema.DescribeFieldResult getFieldDescribe(String objectName, String fieldName) {
```

***
## Javadocs things that might be nice in ApexDocs
| Tag | Usage | Applies to... | Added |
|-----|-------|---------------|-------|
| @see _reference_ |Provides a link to other element of documentation.|Class, Interface, Enum, Field, Method|
| @throws _classname description_ | Describes an exception that may be thrown from this method. | Method|
| @deprecated _description_ | Describes an outdated method. | Class, Interface, Enum, Field, Method | 2019-01-05
| {@inheritDoc} | Copies the description from the overridden method. | Overriding Method |
| {@link reference} |Link to other symbol. | Class, Interface, Enum, Field, Method |
| {@linkplain reference} | Identical to {@link}, except the link's label is displayed in plain text than code font. | Class, Interface, Enum, Field, Method |
| {@value #STATIC_FIELD} | Return the value of a static field. | Static Field |
| {@code literal} | Formats literal text in the code font. It is equivalent to <code>{@literal}</code>. | Class, Interface, Enum, Field, Method |
| {@literal literal} | Denotes literal text. The enclosed text is interpreted as not containing HTML markup or nested javadoc tags. | Class, Interface, Enum, Field, Method|
| {@serial literal} | Used in the doc comment for a default serializable field. | Field |
