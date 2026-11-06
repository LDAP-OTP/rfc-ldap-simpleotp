---
title: "Lightweight Directory Access Protocol: Simple Authentication with OTP"
abbrev: "LDAP: Simple OTP"
category: info

docname: draft-joestr-ldapotpwg-ldapsimpleotp-latest
submissiontype: independent  # also: "independent", "editorial", "IAB", or "IRTF"
number:
date:
consensus: false
v: 3
# area: AREA
# workgroup: LDAP OTP Working Group
keyword:
 - LDAP
 - Simple Authentication
 - One-Time Password
 - OTP
venue:
#  group: LDAP OTP
#  type: Working Group
#  mail: mb.ldap-otp@joestr.priv.at
#  arch: https://github.com/LDAP-OTP
  github: "LDAP-OTP/rfc-ldap-simpleotp"
  latest: "https://LDAP-OTP.github.io/rfc-ldap-simpleotp/draft-joestr-ldapotpwg-ldapsimpleotp.html"

author:
 -
    fullname: Joel Strasser
    organization: n/a
    email: strasser999@gmail.com

normative:

informative:

...

--- abstract

This document describes an additional authentication choice for the
Lightweight Directory Access Protocol (LDAP) which consists of
credentials in the form of name, password, and a one-time password (OTP).

--- middle

# Introduction {#intro}

The Lightweight Directory Access Protocol (LDAP) [RFC4510](https://www.rfc-editor.org/info/rfc4510/) is a
protocol for accessing directories. It offers searching, fetching,
and manipulating directory content and ways to access a set of
security functions.

The LDAP also offers to Login, or in LDAP terminology 'Bind operation', to
a given set of credentials.

These credentials are represented by the 'AuthenticationChoice' defined in
[RFC 4511](https://www.rfc-editor.org/info/rfc4511).

# LDAP Bind operation

The 'Bind operation' [(RFC 4511, Section 4.2)](https://www.rfc-editor.org/info/rfc4511/#section-4.2) defines the authentication choice freely.

The 'Bind request' is defined as follows:

  BindRequest ::= [APPLICATION 0] SEQUENCE { \
    version                 INTEGER (1 ..  127), \
    name                    LDAPDN, \
    authentication          AuthenticationChoice }

# Simple Authentication Method with OTP

The 'Simple Authentication Method with OTP', or short 'Simple OTP', is a way to present the LDAP
server a password and a one-time password (OTP).

The Authentication scope is defined as:

  AuthenticationChoice ::= CHOICE { \
    simple                  [0] OCTET STRING, \
                            -- 1 and 2 reserved \
    sasl                    [3] SaslCredentials, \
    simpleotp               [4] SimpleOtp, \
    ... }

  SimpleOtp ::= SEQUENCE { \
    password                OCTET STRING, \
    onetimepassword         OCTET STRING }

Text based passwords and one-time password transferred to the server using the 'simpleotp' 'AuthenticationChoice' SHALL
be transferred as UTF-8 [RFC3629](https://www.rfc-editor.org/info/rfc3629/) encoded Unicode.

# Conventions and Definitions

{::boilerplate bcp14-tagged}


# Security Considerations {#security}

TODO Security


# IANA Considerations {#iana}

IANA SHOULD assign a new 'Bind authentication' method with following properties:

* Method: simpleotp
* Value: 4
* Owner: IESG
* Usage: LIMITED USE
* Reference: This RFC


--- back

# Acknowledgments
{:numbered="false"}

TODO acknowledge.
