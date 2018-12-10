# Developing
## Common

### Code Style

[Naming for Adapter Pattern](https://softwareengineering.stackexchange.com/questions/361777/how-to-name-different-components-in-adapter-pattern) - good name option is **FooFromBar** or **FooFromBarAdapter**.  

## PHP

### Language

#### Resources

[marcelgsantos/learning-oop-in-php](https://github.com/marcelgsantos/learning-oop-in-php) - A collection of resources to learn object-oriented programming and related concepts for PHP developers.

#### Niceties

**The + operator** - Add items from right-hand array to the left-hand array. The right-hand array item will be added only if the left-hand array does not contain suitable key, otherwise the item will be ignored. There is no difference between numeric and non-numeric keys.
Example: building a config array, where the left-hand array contains only changed parameters, and the right-hand array contains all possible parameters with default values.

#### Extend

[Pre](https://preprocess.io/) - Pre is a PHP preprocessor, designed to make adding new syntax effortless. Flexible integration via Composer.

#### Micro-optimization
[$array[] = $value vs array_push($array, $value)](https://stackoverflow.com/posts/559859/revisions) - *$array[]* is about two times faster, because there is no overhead of calling a function.

# Using
## System

### Midnight Commader

#### RTFM
- [Use Midnight Commander like a pro](http://klimer.eu/2015/05/01/use-midnight-commander-like-a-pro/)
- [Midnight Commander Tips and Tricks](http://www.softpanorama.org/OFM/MC/mc_tips.shtml)

#### Settings
- Settings will be stored in the *~/.config/mc/ini*
- Datetime format - *timeformat_old* (datetime < now - 6 months) and *timeformat_recent* (datetime > now - 6 month). Example of format: `%Y-%m-%d %H:%M`
