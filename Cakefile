# ================
# = Requirements =
# ================
# require 'sys'
{spawn, exec} = require 'child_process'

# ============
# = Function =
# ============
runCommand = (name, args...) ->
  proc =           spawn name, args
  proc.stderr.on   'data', (buffer) -> console.error buffer.toString()
  proc.stdout.on   'data', (buffer) -> console.log buffer.toString()
  proc.on          'exit', (status) -> process.exit(1) if status isnt 0


# =============
# = Constants =
# =============
NAME = "CSV"
RELESE_PATH = "release/"

# ============
# = Watchers =
# ============
task 'test:watch', 'Watch specs and build them', (options) ->
  runCommand 'coffee', '-wc', 'test/specs'

task 'src:watch', 'Watch source files and compile to build', (options) ->
  runCommand 'coffee', '-o', 'lib', '-wc', 'src'

# ============
# = Pack it! =
# ============
task 'pack', 'Pack eveting in a single file', (options)->
  invoke "clean",options
  runCommand 'coffee', '-o', 'lib', '-bc', 'src'
  exec 'mkdir -p '+RELESE_PATH+' && uglifyjs lib/'+NAME+'.js > '+RELESE_PATH+NAME+'.min.js'

task "clean","clean up packing stuff", (options)->
  exec "rm -rdf "+RELESE_PATH