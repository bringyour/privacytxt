# privacy.txt: Privacy policies in the open

The current state of privacy policies is hard to use.

All sites must include a link to their policy on the user-facing page, which must in turn disclose third party policies. With advances in LLMs and AI, it would seem now possible for normal humans to ask questions from a privacy policy and get plain language answers.

For example,

**What are the allowed uses of my data?**

**My data is shared with whom?**

*However*, there are several shortcomings all having to do with the way the privacy policies are presented making them hard to use:

1. It is difficult to get a plain text version of a privacy policy. Some popular consumer sites go so far to create interactive policies with windows that open subsections. Some policies have region-specific supplemental policies (and even multiple levels of supplemental policies) that open into separate pages. Putting this all together in a way that tools can ingest is a challenge.

2. Under the hood of an app there are many connections to first party servers and third-party servers. Mapping these connections back to a company is difficult. For example, in a network trace there may be connection to a random server, `api.abc.com`, sending some data from the device to the cloud. What company is this and what privacy policy does this server use? Sometimes the hostname or TLS cert can tell you, but putting this together for potentially dozens of servers is difficult and hard to *completely* audit.

The current state of privacy policies is like a travel voucher that should get you somewhere great but is impossibly difficult to redeem.

Can you relate?


## privacy.txt

This site proposes a simple solution to the above problem.

The proposal is to map privacy policy **text files** to every host, so that:

1. `<host>/privacy.txt` returns a policy for every connection from an app where data is sent from the device to the cloud. Of course, first parties can only implement this for their servers, but over time first parties who believe in this can require that their third-party dependencies also comply.

2. `<host>/privacy.txt` is a complete, plain text policy that bundles all the sub policies and disclosures in one document. There should be no links to supplemental policies in this document since all should be included in the document itself.


## How to implement

It's quite simple.

On your main site, `abc.com`, host a text version of your policy, `abc.com/privacy.txt`. The section [How to convert a bunch of DOCX to plain text](how-to-convert-a-bunch-of-docx-to-plain-text) can be a start on how to wrangle this from your legal folder.

On your supporting sites, `api.abc.com` etc., add a 303 redirect from `/privacy.txt` to the version hosted on the main site.

## Examples

You can see this in action at

[https://bringyour.com/privacy.txt](https://bringyour.com/privacy.txt)

[https://api.bringyour.com/privacy.txt](https://api.bringyour.com/privacy.txt)


## How to convert a bunch of DOCX to plain text

If you have a bunch of privacy policy DOCX from legal and want to make them more accessible, the following command can convert them into a single TXT file.

```
pandoc -f docx -t plain YOUR_POLICY.docx SUPPLEMENTAL_POLICY1.docx SUPPLEMENTAL_POLICY2.docx -o privacy.txt
```

## Feedback

Comments and discussion welcome in issues or email me at brien@bringyour.com.

&#x2B50; Also [please star this project on GitHub](https://github.com/bringyour/privacytxt) if you support this mission!
