# egovframe-runtime: project context

## Role, scope, and public entry points

`egovframe-runtime` provides reusable eGovFrame Java runtime libraries. Root `README.md`
and `pom.xml` describe the Maven reactor: `Foundation/`, `Integration/`, `Persistence/`,
`Presentation/`, and `Batch/`. Public entry points are the `org.egovframe.rte` Maven artifacts
and Java APIs; affected module README files document module-specific usage. Preserve shared
service, security, persistence, MVC/reactive, and batch contracts when maintaining a module.

## Build and verification evidence

- `README.md` documents JDK 17+, Maven 3.6+, `mvn clean install`, and `mvn test`.
  It also documents running these commands from an individual module directory.
- Root `pom.xml` sets Java release 17, Spring Framework 6.2.11, and the reactor modules.
- `.github/workflows/ci.yml` targets `contribution` pushes/PRs, not `work` pushes.
  Its package matrix uses JDK 17/21 across three OSes and five distributions:
  `mvn -B -Dfile.encoding=UTF-8 -Duser.timezone=Asia/Seoul -U -Dmaven.test.skip=true verify`.
- Its test matrix uses `mvn -B -Dfile.encoding=UTF-8 -Duser.timezone=Asia/Seoul test -pl "$MAVEN_TEST_EXCLUDES"`.
  That workflow explicitly excludes MongoDB, reactive Cassandra, reactive MongoDB, and reactive
  Redis modules because external/embedded stacks are unavailable in CI. Passing the remaining
  matrix does not verify these integrations. Read affected module POM/tests for service requirements.
- CodeQL's build is `mvn -B -Dmaven.test.skip=true compile`; this is not a test run.
- Maven dependencies require configured repository/network access. No service availability or
  successful application test run is established by this card.

## Contribution and submission baseline

`README.md` asks contributors to discuss an issue, fork/branch, write and run tests, and open a PR.
The actual parent is `eGovFramework/egovframe-runtime`; query its current default branch and
fetch that ref before preparing any submission. Record the exact fetched SHA with the change.
Preserve an existing `upstream-submit` branch and open PR. A missing submission branch starts
at that upstream SHA and contains no adoption commit. The fork `work` branch retains tooling.

## Exploration limits

No `.codegraph/` index was present in the clean adoption worktree. Evidence above was obtained
by targeted README, POM, and CI reads; no index or broad tool installation was attempted.


## Maintenance process

Follow [constitution.md](constitution.md) for the domain-card, assessment, planning, verification,
and submission gates. Commands are installed under `.omp/commands/`; read them as agent
instructions. No application build or test was run for tool adoption. Scaffold checks establish
tool installation only, not application correctness.
