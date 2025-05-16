# Convenience globs --------------------------------------------------------
HEADERS_PUBLIC  = glob(["include/libipc/**/*.h"])
HEADERS_PRIVATE = glob(["src/libipc/**/*.h", "src/libipc/**/*.inc"])

# sources common to every platform (sync, core, …)
SRC_COMMON = glob([
    "src/libipc/*.cpp",
    "src/libipc/sync/*.cpp",
    "src/libipc/memory/*.cpp",
])

# Platform-specific source globs -------------------------------------------
SRC_WINDOWS = glob(["src/libipc/platform/win/*.cpp"])
SRC_LINUX   = glob(["src/libipc/platform/linux/*.cpp"])

# Platform selectors -------------------------------------------------------
PLATFORM_WINDOWS = "//platforms:windows_x64"
#PLATFORM_LINUX   = "//third_party/platforms:linux_x64"  # define if/when needed

cxx_library(
    name = "cpp_ipc",

    # ------------- sources -------------
    srcs = SRC_COMMON,
    platform_srcs = [
        (PLATFORM_WINDOWS, SRC_WINDOWS),
        #PLATFORM_LINUX:   SRC_LINUX,
        # add more (aarch64, macOS, …) if you ever build them
    ],

    # ------------- headers -------------
    headers = HEADERS_PUBLIC + HEADERS_PRIVATE,
    header_namespace = "",                       # keep #include paths identical
    include_directories = ["include", "src"],

    # ------------- compile flags -------------
    # No special defines needed for the static build.  If you decide to build a
    # shared DLL later, add:
    # exported_preprocessor_flags = ["LIBIPC_LIBRARY_SHARED_USING__"],
    exported_preprocessor_flags = [],

    # ------------- link style -------------
    preferred_linkage = "static",                # exactly like add_library(... STATIC)

    # ------------- extra system libs on *nix -------------
    #platform_linker_flags = {
    #    PLATFORM_LINUX:   ["pthread", "rt"],     # matches CMake's $<…>:pthread;rt
    #    "//conditions:default": [],              # Windows gets none
    #},

    # ------------- visibility -------------
    visibility = ["PUBLIC"],
)
