import ApiDocGenerator from '@site/src/components/ApiDocGenerator';

<ApiDocGenerator path={props.path} />

export const toc = [
  ...ApiDocGenerator?.toc?.()
]