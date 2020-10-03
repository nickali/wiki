# Tiddlywiki

### Filter Tiddlers by Category and Display Text

```text
<$list filter="[tag[TAG1]tag[TAG2]!search<currentTiddler>] +[sort[title]]">

<$link><h2><b><<currentTiddler>></b></h2></$link>

<$reveal type="nomatch" state={{{ [{!!title}addprefix[$:/state/]addsuffix[-reveal]] }}} text="show"> <$button set={{{ [{!!title}addprefix[$:/state/]addsuffix[-reveal]] }}}  setTo="show">Show</$button> </$reveal>

<$reveal type="match" state={{{ [{!!title}addprefix[$:/state/]addsuffix[-reveal]] }}} text="show"> <$button set={{{ [{!!title}addprefix[$:/state/]addsuffix[-reveal]] }}} setTo="hide">Hide</$button> {{||$:/core/ui/ViewTemplate/body}} </$reveal>

</$list>
```

Initially this lists all the titles of tiddlers that match the filter and a Show/Hide button with the text collapsed. 

