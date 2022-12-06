/*
 * Copyright (c) 2011-present Sonatype, Inc. All rights reserved.
 * Includes the third-party code listed at http://links.sonatype.com/products/clm/attributions.
 * "Sonatype" is a trademark of Sonatype, Inc.
 */
@Library(['private-pipeline-library', 'jenkins-shared', 'iq-pipeline-library']) _

make(
  agentLabel: 'ubuntu-zion',
  javaVersion: 'Java 8',
  mavenVersion: 'Maven 3.6.x',
  useEventSpy: false,
  usePMD: false,
  useCheckstyle: false,
  useInstall4J: false,
  testResults: ['**/target/*-reports/*.xml'],
  deployBranch: 'main',
  runFeatureBranchPolicyEvaluations: true,
  iqPolicyEvaluation: { stage ->
    nexusPolicyEvaluation iqStage: stage, iqApplication: 'neuvector-scanner',
        // maven artifacts are picked up via output of clm:index goal
        iqScanPatterns: [[scanPattern: 'scan-nothing']],
        failBuildOnNetworkError: true
  },
  distFiles: [
    includes: [
      '**/target/ahc-service*.jar',
      'application-check/target/application-check*.jar*',
      'application-check-app/target/media/application-check*',
      'application-check-app/target/gpg/**/application-check*.asc',
      'ahc-lambda-scanner/target/ahc-lambda-scanner*.jar*'
    ],
    excludes: [
      '**/*-sources.jar*',
      '**/*-tests.jar*',
      '**/*-javadoc.jar*'
    ]
  ],
  releaseRetentionPolicy: RetentionPolicy.TEN_BUILDS
)