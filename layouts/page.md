{{- $params := partial "function/params.html" -}}
{{- $author := .Store.Get "author" | default (partial "function/get-author-map.html" .Params.author) -}}
# {{ cond (.Param "capitalizeTitles") (title .Title) .Title }}

{{ if $params.password -}}
  _**{{ T "single.encryptedAbstract" }}**_
{{- else -}}
  {{ .RawContent | replaceRE "\n?{{% fixit-encryptor .+ %}}((\n|.)*){{% /fixit-encryptor %}}\n?" "" }}
{{- end }}

---

> {{ T "single.author"}}: {{ with $author.link }}[{{ $author.name }}]({{ . }}){{ else }}{{ $author.name }}{{ end }}  
> URL: {{ .Permalink }}  
{{ if $params.repost.enable | and (hasPrefix $params.repost.url "http") }}> {{ T "single.repost" }} URL: {{ $params.repost.url }}{{ end }}
