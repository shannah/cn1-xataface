# Codename One Xataface Library

A web service client library that allows [Codename One](http://www.codenameone.com) to connect to a [Xataface](http://xataface.com) application.

## License

Apache License 2.0

## Requirements

1. Compatible with all platforms of Codename One. Doesn't require anything special on the client side.
2. Requires the latest Xataface from github on the server side.

## Installation

Copy the [cn1-xataface.cn1lib](https://github.com/shannah/cn1-xataface/blob/master/bin/cn1-xataface.cn1lib?raw=true) into your project's "lib" directory, and select "Refresh cn1libs".

## Usage

To begin, create an `XFClient` for your app to use.

~~~~
XFClient client = new XFClient("http://example.com/myapp/index.php");
~~~~

Where the URL provided points to the index.php file of a Xataface application.

### Finding Records

Use the `XFQuery` class to build a query, then use the `client.find()` method to retrieve the results.

~~~~
XFQuery query = new XFQuery("gcd_series")
        .contains("name", "Transformers")
        .sort(XFQuery.SortOrder.DESCENDING, "year_began")
        .select("name", "issue_count", "year_began", "year_ended")
        .findAll();
client.find(query, rowset -> {
    // Do something with the rowset  (an XFRowSet object or null)
});
~~~~


The above query would find all records in the gcd_series table where the "name" column contains the text "Transformers".  
Results would be sorted on the year_began column in descending order (most recent first). Only the name, issue_count, year_began, and year_ended 
fields would be included in this rowset.  If we omitted the `select()` call, it would return all of the columns.

### Authentication

`XFClient` includes `setUsername()` and `setPassword()` methods which allow you to hard-code the user information
for connecting to the Xataface app.  But if you leave these null, it will automatically prompt the user to enter their username
and password, which may be preferable in most cases.

### Saving Records

~~~~
client.save(record, r->{
   // If successful, "r" will be an XFRecord object with the updated record.
   // if fail, it will be null 
});
~~~~

### Deleting Records

~~~~
client.delete(record, res->{
    // If successful res will be true.  False otherwise.
});
~~~~


** UNDER CONSTRUCTION**

More docs to come.

## References

* [Xataface Website](http://xataface.com)
* [Codename One Website](http://www.codenameone.com)

## Credits

Created and maintained by [Steve Hannah](http://sjhannah.com)