# Documentation AI experience

For command line we went to https://gitingest.com/ and pointing it the command line tool for innabox https://github.com/innabox/fulfillment-cli then downloaded the contents and pasted into a number of prompts:
- the [gemini2.5](gemini2.5-nocite.md) doc was generated with gemini 2.5 pro with the prompt "please provide documentation in markdown supported by github for using the command line tool" and then adding the prompt Your response must not contain any citation markers.
  - we got the following example [yaml](gemini-yaml.md) then asked "can you provide example yaml for a cluster, your response must not contain any citation markers"

- the [chatgpt4.o](chatgpt-try1.md) doc was generated chatgpt4.0 with "please provide documentation in markdown supported by github for using the command line tool"
   - the more detailed [doc](chatgpt-details.md) using "can you provide more detailed documentation with all the command options"
   - we got the following example [yaml](chatgpt-yaml.md) then asked "can you provide example yaml for a cluster"
- the following was generated using [DeepWiki](https://deepwiki.com/innabox/fulfillment-cli/5.2-data-types) we then generated the following [documentation](deepwiki-nolnk.md) with the prompt "can you generate documentation for this repo using markdown suitable for github without links after code blocks"
