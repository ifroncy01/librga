# librga - Rockchip RGA (Raster Graphic Acceleration) userspace library
#
# This is a packaging-only meson.build for the prebuilt librga.so.
# The source is not publicly available. This build system installs
# the prebuilt library, headers, and pkg-config file.

project('librga', 'c', 'cpp',
    version: '2.1.0',
    default_options: ['buildtype=release'],
)

pkg = import('pkgconfig')

# Install the prebuilt shared library
rga_lib_dir = meson.current_source_dir() / 'libs' / 'Linux' / 'gcc-aarch64'
librga_so = rga_lib_dir / 'librga.so'

# Copy prebuilt .so to build dir for linking
librga = shared_library('rga',
    objects: [],
    install: true,
    soversion: '2',
    version: '2.1.0',
)

# We install the prebuilt binary as a post-install step
# and create proper symlinks
install_script = find_program('sh')

meson.add_install_script(
    install_script, '-c',
    'cp ' + librga_so + ' ${DESTDIR}${prefix}/@0@/librga.so.2.1.0'.format(
        get_option('libdir')),
)

meson.add_install_script(
    install_script, '-c',
    'ln -sf librga.so.2.1.0 ${DESTDIR}${prefix}/@0@/librga.so.2 && '
    'ln -sf librga.so.2 ${DESTDIR}${prefix}/@0@/librga.so'.format(
        get_option('libdir')),
)

# Install headers
install_headers(
    'include/rga.h',
    'include/drmrga.h',
    'include/GrallocOps.h',
    'include/RgaApi.h',
    'include/RgaMutex.h',
    'include/RgaSingleton.h',
    'include/RgaUtils.h',
    'include/RockchipRga.h',
    'include/im2d.h',
    'include/im2d.hpp',
    'include/im2d_buffer.h',
    'include/im2d_common.h',
    'include/im2d_expand.h',
    'include/im2d_mpi.h',
    'include/im2d_single.h',
    'include/im2d_task.h',
    'include/im2d_type.h',
    'include/im2d_version.h',
    subdir: 'rga',
)

# Generate pkg-config file
pkg.generate(
    name: 'librga',
    description: 'Userspace interface to Rockchip RGA 2D accelerator',
    version: '2.1.0',
    libraries: librga,
)