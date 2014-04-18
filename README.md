# Razor TorqueBox

This is a package of TorqueBox suitable for running the [Razor server][server].

It is an almost completely unmodified, stock TorqueBox install.  We use a
dedicated TorqueBox/JBoss for Razor since we run it as a separate user; that
privilege boundary makes it unsuitable for use as a shared application host --
though nothing else does.

## Upgrading TorqueBox versions

Upgrading is a fairly simple process:

1. Replace the zip file with the newer release.
2. Modify `ext/debian/rules` to reflect the new version number.
3. Modify `ext/redhat/razor-torquebox.spec.erb` to reflect the new version number.
4. Extract `jboss/standalone/configuration/standalone.xml` and merge any
   relevant changes into our custom `standalone.xml` configuration file.

