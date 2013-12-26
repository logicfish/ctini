# CtIni

## Usage

Simply import `ctini.ctini`, instantiate IniConfig with the file name of an INI file,
and assign it to a variable.

Don't forget to set the include path with th -J option for DMD, or the stringImportPaths setting for dub

See the example below for how to access the settings.

## Example

INI file:

    [Section]
    ;A comment
    intValue = 3        #Also a comment
    stringValue = "string"
    floatvalue	=123.45 ; <-- flexible whitespace
    [Section.Subsection]
    boolValue = false

D file:

    import ctini.ctini;

    enum config = IniConfig!"config.ini";

    void main() {
        //Four data types
        //Everything available at compile time
        static assert(config.Section.intValue == 3);
        static assert(config.Section.stringValue == "string");
        static assert(config.Section.floatValue == 123.45f);
        static assert(config.Section.Subsection.boolValue == false);
    }

## Notes

 - Variable and section names should follow D identifier rules, and cannot be D keywords.

 - Every variable must be in a section (there must be a section heading before any variables are set).

 - A section cannot have two variables with the same name, but two different sections can have
   variables with the same name.

 - The final object is a `std.typecons.Tuple`, and can be used accordingly.

 - Running app.d with dub will allow you to regenerate the INI grammar, but this should only be 
   necessary if you decide to edit `include/INI.peg`.

## TODO

 - Settings without sections
 - Single quote strings
 - Nicer errors
