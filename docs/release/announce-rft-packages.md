Ready for Testing Announcements
===============================

Per our [community testing policy](/policy/community-testing), we must send weekly digests of packages that are ready
for testing.

Create the Announcement
-----------------------

### Step 1: Identify the packages that are "Ready for Testing"

Run `0-generate-pkg-list` from a machine that has your koji-registered user certificate:

```bash
VERSIONS="<VERSION(S)>"
```
```bash
git clone https://github.com/opensciencegrid/release-tools.git
cd release-tools
0-generate-pkg-list $VERSIONS
```

!!! note
    In the future, will we have a command the produces the package list sorted according to release series and
    importance.

### Step 2: Populate the Announcement Template

Place packages into the appropriate section depending on release series and importance of the package.
The major packages are listed in the [community testing policy](/policy/community-testing).
Omit any packages that do not need to tested by the community such `osg-version` and internal tools.

### Step 3: Send the "Ready for Testing" Announcement

The announcement goes to:

-   `osg-sites@opensciencegrid.org`
-   `cms-t2@fnal.gov`
-   `usatlas-t2-l@lists.bnl.gov`
-   OIM administrative contacts

Use the [osg-notify tool](https://opensciencegrid.org/operations/services/sending-announcements/)
on `osg-sw-submit.chtc.wisc.edu` to send the release announcement using the following command:

    :::console
    $ osg-notify --cert your-cert.pem --key your-key.pem \
        --no-sign --type production --message <PATH TO MESSAGE FILE> \
        --subject 'OSG Packages Available for Testing' \
        --recipients "osg-sites@opensciencegrid.org cms-t2@fnal.gov usatlas-t2-l@lists.bnl.gov" \
        --oim-recipients resources --oim-recipients vos --oim-contact-type administrative

Announcement Template
---------------------

The following email template is filled out to announce that packages are ready for testing.
Text between `<ANGLE BRACKETS>` should be replaced and sections without packages to be tested should be omitted.

```
Several packages are available for testing for tentative release next week.

OSG 3.5 Only:
-   Major Components*
    -   Major Package n.v.r (Comment, Security, etc.)
    -   Major Package n.v.r
-   Minor Components
    -   Minor Package n.v.r
    -   Minor Package n.v.r

Both OSG 3.5 and 3.4:
-   Major Components*
    -   Major Package n.v.r (Comment, Security, etc.)
    -   Major Package n.v.r
-   Minor Components
    -   Minor Package n.v.r
    -   Minor Package n.v.r

OSG 3.4 Only:
-   Major Components*
    -   Major Package n.v.r (Comment, Security, etc.)
    -   Major Package n.v.r
-   Minor Components
    -   Minor Package n.v.r
    -   Minor Package n.v.r

To install any of these packages, run the following command:

    # yum install --enablerepo=osg-testing <PACKAGE NAME>

Please test this software and send positive or negative feedback to
osg-software@opensciencegrid.org.  Be sure to include details describing your
testing platform, e.g. OSG 3.4 vs 3.5, EL6 vs EL7! If you any questions, you can
always contact us at help@opensciencegrid.org.

JIRA Ticket Summary: https://opensciencegrid.atlassian.net/issues/?filter=12355

Sincerely,
The OSG Software & Release Team

* As described by our Community Software Testing Policy,
(https://opensciencegrid.org/technology/policy/community-testing/)
major components of the OSG Software Stack need positive feedback and
the approval of the release manager before they can be released.
```