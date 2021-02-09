libphonenumber
==============

[![PkgGoDev](https://pkg.go.dev/badge/github.com/shortcut/libphonenumber)](https://pkg.go.dev/github.com/shortcut/libphonenumber)
[![GitHubActions](https://github.com/shortcut/libphonenumber/workflows/Test/badge.svg)](https://github.com/shortcut/libphonenumber/actions?query=workflow%3ATest)


golang port of [Google's libphonenumber](https://github.com/google/libphonenumber)

This is a port of https://github.com/ttacon/libphonenumber

Forked to add go module-version.

Status
======

This library is fully stable and is used in production.  
When [Google's libphonenumber](https://github.com/google/libphonenumber) is updated, run `make update`, commit `metagen.go`, and push a new sem-ver tag, and then run `make docs`, to distribute the version.

Examples
========

Super simple to use.

### To get a phone number

```go
num, err := libphonenumber.Parse("6502530000", "US")
```

### To format a number

```go
// num is a *libphonenumber.PhoneNumber
formattedNum := libphonenumber.Format(num, libphonenumber.NATIONAL)
```

### To get the area code of a number
```go
// Parse the number.
num, err := libphonenumber.Parse("1234567890", "US")
if err != nil {
        // Handle error appropriately.
}

// Get the cleaned number and the length of the area code.
natSigNumber := libphonenumber.GetNationalSignificantNumber(num)
geoCodeLength := libphonenumber.GetLengthOfGeographicalAreaCode(num)

// Extract the area code.
areaCode := ""
if geoCodeLength > 0 {
        areaCode = natSigNumber[0:geoCodeLength]
}
fmt.Println(areaCode)
```