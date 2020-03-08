#####################
Maven Central Release
#####################

Thanks to ielis for the tutorial, which is adapted/summarized here

1. Create `JIRA <https://issues.sonatype.org/secure/Signup!default.jspa>`_ account
2. Generate PGP key. All jar files must be signed with the PGP key. To do so, install GPG and then create the key. ::

  gpg --gen-key

Select RSA key. 2048 bits is fine. Set some expiration date, provide a name, an e-mail, and a phrase/comment/description
Then select Passphrase - this is similar to password to SSH private key.

To see all your keys, enter. ::

  gpg --list-keys

Note the hex string (fingerprint).
distribute the key (Maven central needs your public key in order to verify that JARs are signed by you), here with an example (lowest 32 bits of the hexstring, i.e., the last 8 characters). ::

  gpg --keyserver hkp://pool.sks-keyservers.net --send-keys 4AA790FE

add this information to the ``settings.xml`` file that is located in your local maven repository, e.g., ``.m2/settings.xml``. See ielis tutorial for more details, including information about setting up the pom file.

Deploy
~~~~~~
1. To prepare the release, enter (in develop branch). ::

  $ mvn release prepare
  
This updates the versions in the pom files.

2. pull request, merge develop to master

3. do the deploy! ::

  $ mvn -DperformRelease=true clean deploy
  
This will ask for your local admin password and then will test and deploy the release. If all goes well you should see BUILD SUCCESS.

4. Now login to the sonatype website: https://oss.sonatype.org/

5. go to Build promotion | Staging repositories and scroll down where your deployed files should be
present

6. select the deployed repository and hit ``Close`` to run validation

7. monitor progress, where errors may appear (in the case that not all conditions specified above were
satisfied). In that case Drop the repository, fix errors and mvn -DperformRelease=true clean deploy
again

8. having passed through all validations hit the Release button and the new release should appear in
Maven Central Repository within a few hours!
