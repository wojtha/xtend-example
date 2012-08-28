fs            = require 'fs'
{print}       = require 'util'
{spawn, exec} = require 'child_process'
watch         = require 'directory-tree-watcher'

node = null
dnsNode = null

stream = (command, options, callback) ->
  sub = spawn command, options
  sub.stdout.on 'data', (data) -> print data.toString()
  sub.stderr.on 'data', (data) -> print data.toString()
  sub.on 'exit', (status) -> callback?() if status is 0
  sub

start = (file) ->
  node?.kill()
  options = [file]
  node = stream 'coffee', options

task 'run', 'Run server', ->
  start('app.coffee')
  watch 'lib', (event, file) ->
    start('app.coffee')
