_**IMPORTANT NOTE:**_ This project is currently in beta and the documentation is currently incomplete. Please bear with us while the documentation is being written.

####SuperScript offers a means of declaring assets in one part of a .NET web solution and have them emitted somewhere else.


When developing web solutions, assets such as JavaScript declarations or HTML templates are frequently written in a location that differs from their desired output location.

For example, all JavaScript declarations should ideally be emitted together just before the HTML document is closed. And if caching is preferred then these declarations should be in an external file with caching headers set.

This is the functionality offered by SuperScript.



###A Storage Implementation for `SuperScript.ExternalFile`

The [documentation](https://github.com/Supertext/SuperScript.ExternalFile/blob/master/README.md#relocate-assets-into-a-separate-file) 
for `SuperScript.ExternalFile` explains the whys and wherefores of relocating assets to a separate file.

This project simply offers the means of utilising MySQL as the underlying store.

##What's in this project?

`SuperScript.ExternalFile.MySql.MySqlStoreProvider`

  An implementation of `SuperScript.ExternalFile.Storage.IDbStoreProvider` which has the required methods for storing and 
  retrieving the contents for the separate file.
  
  This class shold be configured either in the _web.config_ using
  
  ```XML
  <superScript.ExternalFile>
    <storage type="SuperScript.ExternalFile.Storage.DbStore, SuperScript.ExternalFile">
    		<dbProvider connectionStringName="myConnString" type="SuperScript.ExternalFile.MySql.MySqStoreProvider, SuperScript.ExternalFile.MySql" />
    </storage>
  </superScript.ExternalFile>
  ```
  or in code using
  
  ```C#
  var dbStore = new DbStore();
  dbStore.DbStoreProvider = new SuperScript.ExternalFile.MySql.MySqlStoreProvider();
  SuperScript.ExternalFile.Configuration.Settings.Instance.StoreProvider = dbStore;
  ```

##Dependencies
There are a variety of SuperScript projects, some being dependent upon others.

* [`SuperScript.Common`](https://github.com/Supertext/SuperScript.Common)

  This library contains the core classes which facilitate all other SuperScript modules but which won't produce any meaningful 
  output on its own.

* [`SuperScript.ExternalFile`](https://github.com/Supertext/SuperScript.ExternalFile)

  This project offers the base functionality for relocating assets to an separate file while writing an appropriate reference 
  to this file in the HTML. 
  

`SuperScript.ExternalFile.MySql` has been made available under the [MIT License](https://github.com/Supertext/SuperScript.ExternalFile.MySql/blob/master/LICENSE).
