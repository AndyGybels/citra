add_library(audio_core STATIC
    audio_core.cpp
    audio_core.h
    codec.cpp
    codec.h
    hle/common.h
    hle/dsp.cpp
    hle/dsp.h
    hle/filter.cpp
    hle/filter.h
    hle/mixers.cpp
    hle/mixers.h
    hle/pipe.cpp
    hle/pipe.h
    hle/source.cpp
    hle/source.h
    interpolate.cpp
    interpolate.h
    null_sink.h
    sink.h
    sink_details.cpp
    sink_details.h
    time_stretch.cpp
    time_stretch.h

    $<$<BOOL:${SDL2_FOUND}>:sdl2_sink.cpp sdl2_sink.h>
)

create_target_directory_groups(audio_core)

target_link_libraries(audio_core PUBLIC common core)
target_link_libraries(audio_core PRIVATE SoundTouch)

if(SDL2_FOUND)
    target_link_libraries(audio_core PRIVATE SDL2)
    target_compile_definitions(audio_core PRIVATE HAVE_SDL2)
endif()
