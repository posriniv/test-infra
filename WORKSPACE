# gazelle:repository_macro repos.bzl%go_repositories
workspace(name = "io_k8s_test_infra")

load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive", "http_file")
load("@bazel_tools//tools/build_defs/repo:git.bzl", "git_repository")

http_archive(
    name = "bazel_toolchains",
    sha256 = "a019fbd579ce5aed0239de865b2d8281dbb809efd537bf42e0d366783e8dec65",
    strip_prefix = "bazel-toolchains-0.29.2",
    urls = [
        "https://mirror.bazel.build/github.com/bazelbuild/bazel-toolchains/archive/0.29.2.tar.gz",
        "https://github.com/bazelbuild/bazel-toolchains/archive/0.29.2.tar.gz",
    ],
)

load("@bazel_toolchains//rules:rbe_repo.bzl", "rbe_autoconfig")

rbe_autoconfig(name = "rbe_default")

http_archive(
    name = "bazel_skylib",
    sha256 = "2ef429f5d7ce7111263289644d233707dba35e39696377ebab8b0bc701f7818e",
    urls = [
        "https://github.com/bazelbuild/bazel-skylib/releases/download/0.8.0/bazel-skylib.0.8.0.tar.gz",
    ],
)

load("@bazel_skylib//lib:versions.bzl", "versions")

versions.check(minimum_bazel_version = "0.27.0")

http_archive(
    name = "com_google_protobuf",
    sha256 = "2ee9dcec820352671eb83e081295ba43f7a4157181dad549024d7070d079cf65",
    strip_prefix = "protobuf-3.9.0",
    urls = ["https://github.com/protocolbuffers/protobuf/archive/v3.9.0.tar.gz"],
)

load("@com_google_protobuf//:protobuf_deps.bzl", "protobuf_deps")

protobuf_deps()

http_archive(
    name = "io_bazel_rules_go",
    sha256 = "ae8c36ff6e565f674c7a3692d6a9ea1096e4c1ade497272c2108a810fb39acd2",
    urls = [
        "https://storage.googleapis.com/bazel-mirror/github.com/bazelbuild/rules_go/releases/download/0.19.4/rules_go-0.19.4.tar.gz",
        "https://github.com/bazelbuild/rules_go/releases/download/0.19.4/rules_go-0.19.4.tar.gz",
    ],
)

http_archive(
    name = "bazel_gazelle",
    sha256 = "7fc87f4170011201b1690326e8c16c5d802836e3a0d617d8f75c3af2b23180c4",
    urls = [
        "https://storage.googleapis.com/bazel-mirror/github.com/bazelbuild/bazel-gazelle/releases/download/0.18.2/bazel-gazelle-0.18.2.tar.gz",
        "https://github.com/bazelbuild/bazel-gazelle/releases/download/0.18.2/bazel-gazelle-0.18.2.tar.gz",
    ],
)

load("@io_bazel_rules_go//go:deps.bzl", "go_register_toolchains", "go_rules_dependencies")

go_rules_dependencies()

go_register_toolchains(
    go_version = "1.13",
    nogo = "@//:nogo_vet",
)

load("@bazel_gazelle//:deps.bzl", "gazelle_dependencies")

gazelle_dependencies()

http_archive(
    name = "io_bazel_rules_docker",
    sha256 = "e513c0ac6534810eb7a14bf025a0f159726753f97f74ab7863c650d26e01d677",
    strip_prefix = "rules_docker-0.9.0",
    urls = ["https://github.com/bazelbuild/rules_docker/archive/v0.9.0.tar.gz"],
)

load("@io_bazel_rules_docker//repositories:repositories.bzl", _container_repositories = "repositories")

_container_repositories()

load("@io_bazel_rules_docker//go:image.bzl", _go_repositories = "repositories")

_go_repositories()

load("@io_bazel_rules_docker//container:container.bzl", "container_pull")

container_pull(
    name = "distroless-base",
    digest = "sha256:e37cf3289c1332c5123cbf419a1657c8dad0811f2f8572433b668e13747718f8",
    registry = "gcr.io",
    repository = "distroless/base",
    tag = "latest",
)

container_pull(
    name = "alpine-base",
    digest = "sha256:bd327018b3effc802514b63cc90102bfcd92765f4486fc5abc28abf7eb9f1e4d",  # 2018/09/20
    registry = "gcr.io",
    repository = "k8s-prow/alpine",
    tag = "0.1",  # TODO(fejta): update or replace
)

container_pull(
    name = "alpine-bash",
    digest = "sha256:d520f733f3d648b81201b28b0f9894ad2940972c516e554958d0177470c6a881",  # 2019/07/29
    registry = "gcr.io",
    repository = "k8s-testimages/alpine-bash",
    tag = "latest",  # TODO(fejta): update or replace
)

container_pull(
    name = "boskosctl-base",
    digest = "sha256:a23c19a87857140926184d19e8e54812ba4a8acec4097386ca0993a248e83f8b",  # 2019/08/05
    registry = "gcr.io",
    repository = "k8s-testimages/boskosctl-base",
    tag = "latest",  # TODO(fejta): update or replace
)

container_pull(
    name = "gcloud-base",
    digest = "sha256:8e51eea50a45c6be2a735be97139f85a04c623ca448801a317a737c1d9917d00",  # 2019/08/16
    registry = "gcr.io",
    repository = "cloud-builders/gcloud",
    tag = "latest",
)

container_pull(
    name = "git-base",
    digest = "sha256:01b0f83fe91b782ec7ddf1e742ab7cc9a2261894fd9ab0760ebfd39af2d6ab28",  # 2018/07/02
    registry = "gcr.io",
    repository = "k8s-prow/git",
    tag = "0.2",  # TODO(fejta): update or replace
)

container_pull(
    name = "python",
    digest = "sha256:594a43a1eb22f5a37b15e0394fc0e39e444072e413f10a60bac0babe42280304",  # 2019/08/16
    registry = "index.docker.io",
    repository = "library/python",
    tag = "2",
)

container_pull(
    name = "gcloud-go",
    digest = "sha256:0dd11e500c64b7e722ad13bc9616598a14bb0f66d9e1de4330456c646eaf237d",  # 2019/01/25
    registry = "gcr.io",
    repository = "k8s-testimages/gcloud-in-go",
    tag = "v20190125-cc5d6ecff3",  # TODO(fejta): update or replace
)

git_repository(
    name = "io_bazel_rules_k8s",
    commit = "e7ae2825f0296314ac1ecf13e4c9acef66597986",
    remote = "https://github.com/bazelbuild/rules_k8s.git",
    shallow_since = "1565892120 -0400",
)

load("@io_bazel_rules_k8s//k8s:k8s.bzl", "k8s_repositories")

k8s_repositories()

git_repository(
    name = "io_k8s_repo_infra",
    commit = "1fedfadec8ce38e3738e516fb47227f0abd79245",
    remote = "https://github.com/kubernetes/repo-infra.git",
    shallow_since = "1569036205 -0700",
)

# https://github.com/bazelbuild/rules_nodejs
http_archive(
    name = "build_bazel_rules_nodejs",
    sha256 = "9abd649b74317c9c135f4810636aaa838d5bea4913bfa93a85c2f52a919fdaf3",
    urls = ["https://github.com/bazelbuild/rules_nodejs/releases/download/0.36.0/rules_nodejs-0.36.0.tar.gz"],
)

load("@build_bazel_rules_nodejs//:defs.bzl", "yarn_install")

yarn_install(
    name = "npm",
    package_json = "//:package.json",
    quiet = True,
    yarn_lock = "//:yarn.lock",
)

load("@npm//:install_bazel_dependencies.bzl", "install_bazel_dependencies")

install_bazel_dependencies()

load("@npm_bazel_typescript//:index.bzl", "ts_setup_workspace")

ts_setup_workspace()

# Python setup
# pip_import() calls must live in WORKSPACE, otherwise we get a load() after non-load() error
git_repository(
    name = "io_bazel_rules_python",
    commit = "9d68f24659e8ce8b736590ba1e4418af06ec2552",
    remote = "https://github.com/bazelbuild/rules_python.git",
    shallow_since = "1565801665 -0400",
)

# TODO(fejta): get this to work
git_repository(
    name = "io_bazel_rules_appengine",
    commit = "fdbce051adecbb369b15260046f4f23684369efc",
    remote = "https://github.com/bazelbuild/rules_appengine.git",
    shallow_since = "1552415147 -0400",
    #tag = "0.0.8+but-this-isn't-new-enough", # Latest at https://github.com/bazelbuild/rules_appengine/releases.
)

load("@io_bazel_rules_python//python:pip.bzl", "pip_import")

pip_import(
    name = "py_deps",
    requirements = "//:requirements.txt",
)

load("//:py.bzl", "python_repos")

python_repos()

load("//:repos.bzl", "go_repositories")

go_repositories()

load("@bazel_tools//tools/build_defs/repo:git.bzl", "new_git_repository")

new_git_repository(
    name = "com_github_operator_framework_community_operators",
    build_file_content = """
exports_files([
    "upstream-community-operators/prometheus/alertmanager.crd.yaml",
    "upstream-community-operators/prometheus/prometheus.crd.yaml",
    "upstream-community-operators/prometheus/prometheusrule.crd.yaml",
    "upstream-community-operators/prometheus/servicemonitor.crd.yaml",
])
""",
    commit = "efda5dc98fd580ab5f1115a50a28825ae4fe6562",
    remote = "https://github.com/operator-framework/community-operators.git",
    shallow_since = "1568320223 +0200",
)

http_archive(
    name = "io_bazel_rules_jsonnet",
    sha256 = "59bf1edb53bc6b5adb804fbfabd796a019200d4ef4dd5cc7bdee03acc7686806",
    strip_prefix = "rules_jsonnet-0.1.0",
    urls = ["https://github.com/bazelbuild/rules_jsonnet/archive/0.1.0.tar.gz"],
)

load("@io_bazel_rules_jsonnet//jsonnet:jsonnet.bzl", "jsonnet_repositories")

jsonnet_repositories()
