

             VERIFICATUM MIX-NET META DISTRIBUTION

This package contains the VMN distribution and the distributions of
the packages that improve its speed. To compile the software you need
to install the m4 macro processor, and to run the software you need to
install OpenJDK 8. On a clean Ubuntu 16.04 all you need is

    $ sudo apt-get install --yes m4 libgmp-dev openjdk-8-jdk

and correspondingly for other platforms. It now suffices to simply run

    $ sudo make install

which configures, makes, and installs each package in the default
location. Typically this is /usr/local/bin, /usr/local/share/java, and
/usr/local/lib. This also initializes the default random source to
/dev/urandom.

To delete all files that you installed, you can run

    $ sudo make uninstall

You can run all tests using

    $ make check

This takes a long time to complete, so please be patient.

Finally, you can run the demo found in
verificatum-vmn-<VERSION>/demo/mixnet by simply using

    $ make demo

This runs the key generation, generates demo ciphertexts, mixes the
ciphertexts (re-encrypts, permutes, and decrypts), and finally it runs
the reference implementation of the verifier of the universally
verifiable proof.


                          WARNING!

This install script is ONLY INTENDED FOR DEMONSTRATION PURPOSES. For
actual use we strongly suggest that you read the README file of each
separate package and install and verify your installation separately
to make sure that it is installed properly on your system. You must
also make sure that the random source you use is sound.
