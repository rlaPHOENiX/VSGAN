---
title: "Dont!: Pip as Admin"
permalink: /pip-as-admin/
excerpt: "Reasons against using pip under administrator permissions."
last_modified_at: 2021-01-20T23:07:00-00:00
toc: true
classes: wide
---

There are risks and environment annoyances involved with using `pip` under administrator permissions.

Administrator permission can be given via `sudo` or an Administrator Terminal, Shell, or Command-Prompt session.
{: .notice}

## Risks

### Arbitrary Code Execution

The purpose of `pip` is to install/execute python project code from the web (from other users). You could be installing (thus running) code from a malicious project.
While it's common sense to only install projects you trust, running with administrator permission can only exacerbate the problem. There's no benefit to running as administrator other
than to install system-wide for all users to utilize, however, if it's not necessary to be system-wide, then why risk it.

### Double Installations

`pip install` will install to the most applicable Python `site-packages` directory based on the user or it's permissions.

This means if you `pip install` the same package under different users or permissions you may end up with the package being installed on your system more than once.
The System and programs may use the `Administrator` installed packages as priority over the Non-Administrator installed packages.
When updating (via `--upgrade`) the package won't update all installations, it will only update whatever that `pip` call's permissions allows it to update.

## Example scenarios

Here's some example scenario's and what can end up as the result by using pip under administrator permissions when not strictly necessary.

All examples assume the python and pip environment are in a clean and fresh installed state.
{: .notice}

### Updating

1. Run (for example) `pip install example` under administrator permissions.
2. Later on, you wish to update it via `pip install --upgrade example` (or e.g. `example==2.0`), however, this was not run under the same permission it was installed under so it fails to find a package named `example`.
3. This causes pip to ignore the `--upgrade` flag and install the package resulting in it being installed on the users system twice, most likely without the user realizing.
4. This can cause the below example to come into effect.

### Package Environment Priority

The following snippets use Bash syntax, `$` are normal user permissions, `#` are administrator permissions (e.g. called via sudo, su, administrator shell, e.t.c).
{: .notice}

Let's assume we have a package named (for example) `foo`.

1. This package is very simple and has a `__init__.py` which has only `print('The package foo is v{version}')`.
2. Let's assume `{version}` will be the installed `foo`'s version, that is currently running and executing the print.

The following installs foo==1.0 under administrator permissions and runs it under user permissions.

```bash
# pip install foo==1.0
>>> ... it installs foo v1.0 under administrator permissions
$ python -c 'import foo'
>>> 'The package foo is v1.0'
```

The following now tries to upgrade to foo==2.0 and run it, both under user permissions.

```bash
$ pip install foo==2.0
>>> ... `foo` isnt installed under user permissions;
    it installs `foo` v2.0 rather than updating the existing package.
$ python -c 'import foo'
>>> 'The package foo is v1.0'
```

Now why has that stated `'The package foo is v1.0'` when it has installed 2.0, and it even installed it under the same permission environment as it has been called from?

The answer is environment priority. When a system or program tries to execute something, they may loosely define the location of the executable or script and leave it up to the PATH environment variable to decide which executable should be run.
There's two PATH environment variables which will be used, the `User`, and the `System` PATH environment variables. `System` may or may not be checked before User.

The example above would only occur if the `System` PATH environment variable was used first.

For example, when calling `pip`, it is in fact doing exactly this and checking which executable should be run based on the PATH environment variables.
