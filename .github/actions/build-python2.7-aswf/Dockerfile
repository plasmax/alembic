FROM aswf/ci-usd:2019.9

# install auditwheel and dependency
RUN yum install -y patchelf
RUN pip install auditwheel

# TODO: this won't work as Imath 3.0.4 builds 
# build imath dependency (although this comes with ci-usd so should be unnecessary)
RUN git clone --depth 1 --branch v3.0.4 https://github.com/AcademySoftwareFoundation/Imath.git /Imath
RUN mkdir /imathbuild
RUN cd /imathbuild
RUN cmake /Imath -DPYTHON=ON -DUSE_PYTHON2=ON
RUN make
RUN make install

# Setup dev environment
ENV PLAT manylinux2010_x86_64

# Copy build script and build
COPY build_alembic.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh

ENTRYPOINT [ "/entrypoint.sh" ]
