// guggenheim.js build tasks

var fs = require('fs'),
	sys = require('util'),
	uglifyjs = require("uglify-js"),
	path = require('path'),
	exec = require('child_process').exec;

namespace('guggenheim', function(){

	desc('Default build task. Minifies library and creates dist folder.')
	task('build',[],function(){

		if(!fs.existsSync('dist'))
			fs.mkdir('dist')

		var ast = uglifyjs.minify('src/guggenheim.js',{outSourceMap:'guggenheim.min.map'}), // parse code and get the initial AST
			output = fs.openSync('dist/guggenheim.min.js','w+'),
			sourceMap = fs.openSync('dist/guggenheim.min.map','w+')

		fs.writeSync(output,ast.code + "\n //# sourceMappingURL=guggenheim.min.map")
		fs.writeSync(sourceMap,ast.map)
	})

	desc('Runs PhantomJS tests')
	task('test',[],function(){
		function puts(error, stdout, stderr) { sys.puts(stdout) }
		exec('phantomjs test/runner.coffee',puts)
	})
})
