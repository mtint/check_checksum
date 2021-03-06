# Release Workflow

Specify the release version.

```
VERSION=0.3.0
```

Update the version in `check_checksum`:

```
sed -i "s~^version=.*~version='$VERSION'~" check_checksum
```

## Authors

Update the [.mailmap](.mailmap) and [AUTHORS](AUTHORS) files:

```
git checkout master
git log --use-mailmap | grep ^Author: | cut -f2- -d' ' | sort | uniq > AUTHORS
```

## Git Tag

Commit these changes to the "master" branch:

```
git commit -v -a -m "Release version $VERSION"
```

Create a signed tag:

```
git tag -s -m "Version $VERSION" "v$VERSION"
```

Push the branch and tag.

```
git push origin master
git push --tags
```

## GitHub Release

Create a new release for the newly created Git tag.
https://github.com/NETWAYS/check_checksum/releases
