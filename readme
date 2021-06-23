function setup-certs() {
  # place to put the combined certs
  local cert_path="$HOME/.certs/all.pem"
  local cert_dir=$(dirname "${cert_path}")
  [[ -d "${cert_dir}" ]] || mkdir -p "${cert_dir}"
  # grab all the certs
  security find-certificate -a -p /System/Library/Keychains/SystemRootCertificates.keychain > "${cert_path}"
  security find-certificate -a -p /Library/Keychains/System.keychain >> "${cert_path}"
  # configure env vars for commonly used tools
  export GIT_SSL_CAINFO="${cert_path}"
  export AWS_CA_BUNDLE="${cert_path}"
  export NODE_EXTRA_CA_CERTS="${cert_path}"
  # add the certs for npm and yarn
  # and since we have certs, strict-ssl can be true
  npm config set -g cafile "${cert_path}"
  npm config set -g strict-ssl true
  yarn config set cafile "${cert_path}" -g
  yarn config set strict-ssl true -g
}
setup-certs
