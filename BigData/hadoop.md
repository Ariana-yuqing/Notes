# Hadoop - The definition guide. 4th edition

## Serialization

### Writable Classes

fixed-length formats vs. variable-length formats
The variable-length formats use only a single byte to encode the value if it is small enough (between –112 and 127, inclusive); otherwise, they use the first byte to indicate whether the value is positive or negative, and how many bytes follow. For example, 163 requires two bytes:
```Java
byte[] data = serialize(new VIntWritable(163)); 
assertThat(StringUtils.byteToHexString(data), is("8fa3"));  
```
Fixed- length encodings are good when the distribution of values is fairly uniform across the whole value space, such as when using a (well-designed) hash function. 

Most numeric variables tend to have nonuniform distributions, though, and on average, the variable- length encoding will save space. Another advantage of variable-length encodings is that you can switch from VIntWritable to VLongWritable, because their encodings are ac‐ tually the same. So, by choosing a variable-length representation, you have room to grow without committing to an 8-byte long representation from the beginning.
