+++
title = '{{ replace .File.ContentBaseName "-" " " | title }}'
date = {{ .Date }}
description = ''
tag = [
	'',
]
topic = ''
[params]
	article = true
	math = false
featured_image = '{{ .Site.Params.favicon }}'
+++

