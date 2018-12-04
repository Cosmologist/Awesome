# Developing
## Common

### Code Style

[Naming for Adapter Pattern](https://softwareengineering.stackexchange.com/questions/361777/how-to-name-different-components-in-adapter-pattern) - good name option is **FooFromBar** or **FooFromBarAdapter**.  

## PHP

### Language

#### Extend

[Pre](https://preprocess.io/) - Pre is a PHP preprocessor, designed to make adding new syntax effortless. Flexible integration via Composer.

#### Micro-optimization
[$array[] = $value vs array_push($array, $value)](https://stackoverflow.com/posts/559859/revisions) - If you use *array_push()* to add one element to the array it's better to use *$array[]* because in that way there is no overhead of calling a function.

# Using
## System

### Midnight Commader

#### RTFM
- [Use Midnight Commander like a pro](http://klimer.eu/2015/05/01/use-midnight-commander-like-a-pro/)
- [Midnight Commander Tips and Tricks](http://www.softpanorama.org/OFM/MC/mc_tips.shtml)

#### Settings
- Settings will be stored in the *~/.config/mc/ini*
- Datetime format - *timeformat_old* (datetime < now - 6 months) and *timeformat_recent* (datetime > now - 6 month). Example of format: `%Y-%m-%d %H:%M`
