# Signing Xcode

Since Apple no longer loads 3rd party plugins (in Xcode 8 and above), we have to make change to it. What we have to do overall is to re-codesign Xcode. This allows us to load 3rd party plugins. Here are the steps to do so:

1. Close Xcode
    
2. Prepare code sign certificate
   
   2.1 Open "Keychain Access" (in Applications -> Utilities) and select "login" in the left pane.
   
   2.2 Select Create a Certificate ( in KeyChain Access -> Certificate Assistant )
       
   ![Keychaing1](Documents/Images/Keychain1.png)
       
   2.3 Input your name (whatever you like) and select "Code Signing" for Certificate Type.
       Not required but the name is used later in a command line so it could be better to use easily distinguishable name here (I use XcodeSigner here).
       
    ![Keychaing2](Documents/Images/Keychain2.png)
       

  Now you have a certificate to code sign.


3. Re-signing Xcode

   Then in a terminal,

         $ sudo codesign -f -s XcodeSigner /Applications/Xcode.app    (Replace the Xcode path if it is different.)

   This should take a while.
   
4. Build XVim

   Go to XVim directory you cloned and build it as usual (Read INSTALL section in [README.md](README.md)).

5. Certificate Expiration

   A self-signed root certificate has a short expire date (1 year).
   Please check expire date of your certificate `XcodeSigner` in Keychain Access App.
   If it expires, please re-create it.

