### Resources

http://homes.cs.washington.edu/~aczeskis/random/openssl-encrypt-file.html

http://stuff-things.net/2007/06/11/encrypting-sensitive-data-with-ruby-on-rails/


### General Idea

Most sites use username/password, but it requres you to remember passwords and trust the service who may or may not encrypt
it. blah, blah, blah, an asynchronous encryption approach is better. 


### Setup/Registration

The idea of public/private key encryption is that the public key can be used to encrypt messages and the private key can
be used to decrypt them.

The user generates a public and private key on their client, whether through command line with openssh or some GUI (likely a browser plugin). 
One key should be generated for each site they have an account with. When registering for the site, they insert their 
public key which is uploaded to the server. Possibly some simple encryption for the initial upload to the server so that 
there is no chance of a third party getting access to a key.


### Authentication

Once the service has the public key, they can authenticate the user by generating some message unique to the user. A good
message might be their username, some site seed, and a current timestamp all hashed together. The service then encrypts this 
generated message and sends it to the client in response to the initial login request. The client takes this message, 
decrypts it with its private key, and sends it back to the service. 

If  the client's response matches the generated unencrypted message, the user is authenticated. A session cookie is sent
back to the client just as it is with most current sites and the user is enabled to use the site as long as the cookie is
valid.


### Open Questions, Problems

 * You need to take your keys with you wherever you go. Probably an issue on mobile.
 * "Password" recovery is still an issue.
 * Not as easy as just entering a password
 * Many will choose 1Password type solutions for their keychain. Can be an issue if their machine and global password is
   compromized.

