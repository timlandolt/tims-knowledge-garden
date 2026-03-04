---
{"dg-publish":true,"permalink":"/knowledge/devise/","tags":["ruby-on-rails","webdevelopement","auth"]}
---

---

Devise is an authentication for rails based on [[Knowledge/Warden\|Warden]]. 
It is module based and consists of the following 10 modules:

- **Database Authenticatable**: hashes and stores a password in the database to validate the authenticity of a user while signing in. The authentication can be done both through POST requests or HTTP Basic Authentication.
- **Omniauthable**: adds OmniAuth support (OpenID, Facebook, …).
- **Confirmable**: sends emails with confirmation instructions and verifies whether an account is already confirmed during sign in.
- **Recoverable**: resets the user password and sends reset instructions.
- **Registerable**: handles signing up users through a registration process, also allowing them to edit and destroy their account.
- **Rememberable**: manages generating and clearing a token for remembering the user from a saved cookie.
- **Trackable**: tracks sign in count, timestamps and IP address.
- **Timeoutable**: expires sessions that have not been active in a specified period of time.
- **Validatable**: provides validations of email and password. It's optional and can be customized, so you're able to define your own validations.
- **Lockable**: locks an account after a specified number of failed sign-in attempts. Can unlock via email or after a specified time period.

## See also
- [GitHub - scambra/devise\_invitable: An invitation strategy for devise](https://github.com/scambra/devise_invitable)