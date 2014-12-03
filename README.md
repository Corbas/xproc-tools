# XProc Tools #

This is a small set of useful XProc tools that have developed over time to provide a framework for transformation of content from one XML format to another. These are primarily used when transformation makes most sense as a sequence of transformations. 

All of these can be used via the ExPath package file or directly from the `src` directory.

## Namespace ##

All of these steps are in the namespace **`"http://www.corbas.co.uk/ns/xproc/steps"`** (we use the prefix `ccproc`)

## temp-dir.xpl ##

**Import via  `http://www.corbas.co.uk/xproc-tools/temp-dir`**

### ccproc:temp-dir

```xml
<p:declare-step type="ccproc:temp-dir">
  <p:output port="result"/>
  <p:option name="fallback" select="'.'"/>
</p:declare-step>
```

This step attempts to discover the system temporary directory path.  It has no inputs and a single output. The `result`  port provides a `c:result` element that contains the path to the temporary directory (as a URL) when found or an empty `c:result` if not.

```
<p:import href="http://www.corbas.co.uk/xproc-tools/temp-dir">
<ccproc:temp:dir name="get-temp-dir"/>
<p:identity/>
```

```xml
<c:result>file:///tmp/</c:result>
```

### ccproc:temp-file ###

This step creates a temporary file, following the same arguments as the EXProc `pdf:tempfile` step except that the system temporary directory generated by `ccproc:temp-dir` is used  as the temporary file location.

See (???) for additional documentation.

## directory-list.xpl ##

**Import via  `http://www.corbas.co.uk/xproc-tools/directory-list**

###  ccproc:directory-list ###

```xml
<p:declare-step type="ccproc:directory-list">
  <p:output port="result"/>
  <p:option name="path" required="true"/>
  <p:option name="resolve" select="'false'"/>
  <p:option name="match-path" select="'false'"/
  <p:option name="include-filter"/>
  <p:option name="exclude-filter"/>
</p:declare-step>
```

This step slightly extends the standard `p:directory-list` step. 

Firstly, it allows the include and exclude patterns to operate on any part of the file or path name and not to match all of it. Secondly, it does not exclude directories under any circumstance. Directories always pass filtering.

path
:	The path option should point to a directory on the current filesystem. It is down to the underlying implementation as to whether URL schemes bar `file` are supported.


The step also has additional options. 



```
<p:import href="http://www.corbas.co.uk/xproc-tools/directory-list">
<ccproc:temp:dir name="get-temp-dir"/>
<p:identity/>
```
