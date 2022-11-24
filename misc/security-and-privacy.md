# [Self-Review Questionnaire: Security and Privacy](https://w3ctag.github.io/security-questionnaire/)

# Security and Privacy Horizontal Reviews for IMSC-HRM

* PING review: w3cping/privacy-request#65
* Security review: w3c/security-request#18

# Security and Privacy Self-review for IMSC-HRM

This is an edited version of the security and privacy questionnaire template at
https://raw.githubusercontent.com/w3ctag/security-questionnaire/main/questionnaire.markdown as linked from
[Self-Review Questionnaire: Security and Privacy](https://www.w3.org/TR/security-privacy-questionnaire/)

> 01.  What information might this feature expose to Web sites or other parties,
>      and for what purposes is that exposure necessary?

None. The IMSC-HRM is a static-analysis algorithm of IMSC documents.
Executing the algorithm requires no requests to any origins.
The resource that it processes is an IMSC Document Instance.
This specification does not define any protocol or interface for obtaining such a resource,
and it does not define any interface for exposing the results of the analysis.

> 02.  Do features in your specification expose the minimum amount of information
>      necessary to enable their intended uses?

Yes.

> 03.  How do the features in your specification deal with personal information,
>      personally-identifiable information (PII), or information derived from
>      them?

No features interact with, generate or consume personal information or PII.

> 04.  How do the features in your specification deal with sensitive information?

No features interact with, generate or consume sensitive information.

> 05.  Do the features in your specification introduce new state for an origin
>      that persists across browsing sessions?

No.

> 06.  Do the features in your specification expose information about the
>      underlying platform to origins?

No.

> 07.  Does this specification allow an origin to send data to the underlying
>      platform?

No.

> 08.  Do features in this specification enable access to device sensors?

No.

> 09.  Do features in this specification enable new script execution/loading
>      mechanisms?

No.

> 10.  Do features in this specification allow an origin to access other devices?

No.

> 11.  Do features in this specification allow an origin some measure of control over
>      a user agent's native UI?

No.

> 12.  What temporary identifiers do the features in this specification create or
>      expose to the web?

None.

> 13.  How does this specification distinguish between behavior in first-party and
>      third-party contexts?

Not applicable.

> 14.  How do the features in this specification work in the context of a browser’s
>      Private Browsing or Incognito mode?

Not applicable or relevant: features in this specification do not define any browser behaviour.

> 15.  Does this specification have both "Security Considerations" and "Privacy
>      Considerations" sections?

Yes, one section for Privacy and Security Considerations at https://www.w3.org/TR/imsc-hrm/#privacy-and-security-considerations

> 16.  Do features in your specification enable origins to downgrade default
>      security protections?

No.

> 17.  How does your feature handle non-"fully active" documents?

Not applicable or relevant.

> 18.  What should this questionnaire have asked?

No further questions.
