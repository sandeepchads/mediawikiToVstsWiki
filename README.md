# mediawikiToVstsWiki

Prerequisites
- sql backup of your media-wiki + images (or a mediawiki without LDAP integration)
- vsts wiki
- git (https://git-scm.com/download/win)
- Pandoc (https://github.com/jgm/pandoc/releases/tag/2.1.3)

Steps:
1) In case you need to create a local media wiki server (Optional Step - required if your current media wiki is LDAP integrated, but preferred as it will speed things up)
  - creating a mediawiki server
    - Download and install XAMPP, Apache and MySql from https://www.apachefriends.org
    - Download and install 7-Zip from http://www.7-zip.org/download.html
    -	Disable UAC from "C:\windows\System32\UserAccountControlSettings.exe"
    - Download MediaWiki package from https://www.mediawiki.org/wiki/Download
    - Copy the extracted mediawiki files to \htdocs
  
  Alternately, in your existing mediawiki, you change the LocalSettings.php to open it for public 
  
  $wgGroupPermissions['*']['read'] = true;
  
  - Backup your existing mediawiki (https://www.mediawiki.org/wiki/Manual:Restoring_a_wiki_from_backup#Import_the_database_backup)
    - From the command line using mysqladmin
    <pre>mysqladmin -u wikidb_user -p drop wikidb</pre>
    Substituting as appropriate for wikidb_user and wikidb. The -p parameter will prompt you for the password.

   - Then to create a new database:
    <pre>mysqladmin -u wikidb_user -p create wikidb</pre>
    - To import dump_of_wikidb.sql from the command line you simply do:
      <pre>mysql -u wikidb_user -p wikidb < dump_of_wikidb.sql</pre>
    

2) Run the script with the following parameters:
    
    -mu : Your media wiki url <format: http://localhost:8080/mediawiki>,
    
    -ip : Your image backup location <format: C:\xampp\htdocs\mediawiki\images>, 
    
    -u : mediawiki username <format: alias>,
    
    -pwd : mediawiki password,
    
    -au : mediawiki absolute url(can be different from mediawiki url provided above - to change absolute urls in content) <format: https://mywiki.com/index.php\?title=>, 
    
    -o : output directory on disk <format: C:\anylocation\ >,
    
    -r : vsts wiki clone url <format: https://myacct.visualstudio.com/proj/_git/proj.wiki>,
    
    -vstsUserName : vsts username (Please provide PAT token if asked for password),
    
    -pnPath : path where pandoc.exe resides <format: C:\pandoc\>

  
