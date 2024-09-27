# Delphi MMDB Wrapper

Simple Wrapper for the Delphi MMDB Reader library by optinsoft.

I wrote this for myself but decided to publish it. Its very basic and does not offer all the features of the main MMDB reader library.

## Why?

I wanted to use less code to get the country info of an IP address.

## Depends on

* [MMDB Reader](https://github.com/optinsoft/MMDBReader) by Optinsoft

## Example

```pas
procedure TestWrapper;
begin
  var wrapper := TMMDBWrapper.Create;
  try
    // Set MaxMind DB path
    wrapper.DBFilePath := '.\dbip-country-lite-2024-09.mmdb';

    // Test IP
    var aIP := '8.8.8.8';

    // Check if IP is valid
    if wrapper.isValidIPv4(aIP) then
    begin
      // Get Country Info
      var countryInfo := wrapper.GetCountryInfo(aIP);

      // DB Build Date
      Writeln('DB Date: ', DateTimeToStr(wrapper.GetDBBuildDate));

      Writeln('Country ISO: ', countryInfo.ISOCode);
      Writeln('Country Name: ', countryInfo.NameEN);

      // List all country names in different languages
      Writeln('Country Lang Names: ');
      for var aName in countryInfo.Names do
        Writeln(aName.LangCode, ' - ', aName.Name);
    end
    else
      Writeln('Invalid IP: ', aIP);
  finally
    wrapper.Free;
  end;
end;
```