#  _               _ 
# | |__   _____  _(_)
# | '_ \ / _ \ \/ / | MIT & Apache 2.0 dual licensed
# | | | |  __/>  <| | Version 1.3.5
# |_| |_|\___/_/\_\_| https://github.com/EmberEmu/hexi

set(HEXI_HEADERS
    ${CMAKE_CURRENT_SOURCE_DIR}/hexi/hexi.h
    ${CMAKE_CURRENT_SOURCE_DIR}/hexi/exception.h
    ${CMAKE_CURRENT_SOURCE_DIR}/hexi/endian.h
    ${CMAKE_CURRENT_SOURCE_DIR}/hexi/dynamic_buffer.h
    ${CMAKE_CURRENT_SOURCE_DIR}/hexi/dynamic_tls_buffer.h
    ${CMAKE_CURRENT_SOURCE_DIR}/hexi/shared.h
    ${CMAKE_CURRENT_SOURCE_DIR}/hexi/buffer_adaptor.h
    ${CMAKE_CURRENT_SOURCE_DIR}/hexi/buffer_sequence.h
    ${CMAKE_CURRENT_SOURCE_DIR}/hexi/binary_stream.h
    ${CMAKE_CURRENT_SOURCE_DIR}/hexi/static_buffer.h
    ${CMAKE_CURRENT_SOURCE_DIR}/hexi/concepts.h
    ${CMAKE_CURRENT_SOURCE_DIR}/hexi/impl/intrusive_storage.h
    ${CMAKE_CURRENT_SOURCE_DIR}/hexi/file_buffer.h
    ${CMAKE_CURRENT_SOURCE_DIR}/hexi/null_buffer.h
    ${CMAKE_CURRENT_SOURCE_DIR}/hexi/stream_adaptors.h
    ${CMAKE_CURRENT_SOURCE_DIR}/hexi/version.h
    ${CMAKE_CURRENT_SOURCE_DIR}/hexi/pmc/buffer_base.h
    ${CMAKE_CURRENT_SOURCE_DIR}/hexi/pmc/buffer_read.h
    ${CMAKE_CURRENT_SOURCE_DIR}/hexi/pmc/buffer_write.h
    ${CMAKE_CURRENT_SOURCE_DIR}/hexi/pmc/buffer.h
    ${CMAKE_CURRENT_SOURCE_DIR}/hexi/pmc/binary_stream.h
    ${CMAKE_CURRENT_SOURCE_DIR}/hexi/pmc/binary_stream_reader.h
    ${CMAKE_CURRENT_SOURCE_DIR}/hexi/pmc/binary_stream_writer.h
    ${CMAKE_CURRENT_SOURCE_DIR}/hexi/pmc/stream_base.h
    ${CMAKE_CURRENT_SOURCE_DIR}/hexi/pmc/buffer_adaptor.h
    ${CMAKE_CURRENT_SOURCE_DIR}/hexi/pmc/buffer_read_adaptor.h
    ${CMAKE_CURRENT_SOURCE_DIR}/hexi/pmc/buffer_write_adaptor.h
    ${CMAKE_CURRENT_SOURCE_DIR}/hexi/allocators/default_allocator.h
    ${CMAKE_CURRENT_SOURCE_DIR}/hexi/allocators/tls_block_allocator.h
    ${CMAKE_CURRENT_SOURCE_DIR}/hexi/allocators/block_allocator.h
)

set(HEXI_HEADERS ${HEXI_HEADERS} PARENT_SCOPE)
