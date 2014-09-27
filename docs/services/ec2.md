# EC2

Fedimg is hooked into Amazon Web Services and registers images as public AMIs in all
EC2 regions. This page explains the process, which takes place in
`fedimg/services/ec2.py`.

## Terminology

This document makes use of a few terms which may be ambiguous or unfamiliar to
you. This section hopes to avoid confusion.

### Utility instance

The **utility instance** is the instance which downloads the raw image file and
writes it to a volume for later snapshotting. It is the first instance that is
created during the EC2 service.

### Test instance

The **test instance** is launched from the AMI that is registered by an earlier
step. Fedimg can be easily configured to perform tests on this instance to
determine the health of the new AMI. It is the second instance that is created
during the EC2 service.

## Custom exceptions

The EC2 service defines three custom exceptions that can be raised by the service.

-   `EC2ServiceException`, a generic exception (inherits from `Exception`).
-   `EC2UtilityException`, which can arise when there is a problem with the
    utility instance (inherits from `EC2ServiceException`).
-   `EC2TestException`, which can arise when there is an issue with the test
    instance (also inherits from `EC2ServiceException`).