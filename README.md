# third_party.go

third_party.go is a self contained single file that helps with bumping third
party repos and managing the GOPATH.

## Usage

### Setup a repo

```
curl https://raw.github.com/coreos/third_party.go/master/third_party.go > third_party.go
go run third_party.go setup github.com/mygithubname/newproject
git add .
git commit -m "Initial commit"
```

### Build your project

When none of the `third_party.go` subcommands are used it acts simply as a
wrapper around go that sets up the environment variables to GOPATH. So, just
use `build` and your package name.

```
go run third_party.go build -v github.com/mygithubname/newproject
```

### Bumping a package

`third_party.go` helps you bump and manage packages. This will put the goraft
package into your `third_party/src` directory and tell you the git commit that
it came from.

```sh
go run third_party.go bump github.com/goraft/raft
```
```
github.com/goraft/raft c064081f635e519f162280f133faebc1a445106b
```

### Bumping all packages

This will walk all of the packages installed in `third_party/src` and run the
`bump` subcommand on it if it is a valid go pkg.

```
go run third_party.go bump-all
```

## Testing third_party.go

Becuase third_party.go has a `+build ignore` tag at the top you will need to use the
test script to run the unit tests:

```
./test
```
